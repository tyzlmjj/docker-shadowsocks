# docker-shadowsocks-libev

shadowsocks-libev 已经提供了[Docker实现](https://github.com/shadowsocks/shadowsocks-libev/tree/master/docker/alpine)，所以直接使用就可以了


## 启动SS服务

安装好docker并启动，执行下面的命令就会启动一个ss服务,注意修改密码!

```bash
$ docker run -d -e PASSWORD=9MLSpPmNt -p 8388:8388/tcp -p 8388:8388/udp --restart always shadowsocks/shadowsocks-libev:latest
```

可以用`docker ps`命令查看运行的容器。

或者也可以使用docker-compose运行


## docker-compose启动ss服务

**创建一个 `docker-compose.yml` 文件**

```yaml
server:
  image: shadowsocks/shadowsocks-libev:latest
  ports:
    # 设置对外端口
    - "8388:8388/tcp"
    - "8388:8388/udp"
  environment:
    # 密码
    - PASSWORD=9MLSpPmNt
  restart: always
```

:warning: 注意修改端口号和密码

**启动ss服务**
```bash
$ docker-compose up -d
```


## 负载均衡

使用 docker 的集群化处理

**创建一个 `docker-compose.yml` 文件**
```yaml
version: "3"
services:
  ss_server:
    image: shadowsocks/shadowsocks-libev:latest
    deploy:
      #运行容器数量
      replicas: 5
      resources:
        limits:
          #对单个容器的cup和内存的限制
          cpus: "0.1"
          memory: 50M
      restart_policy:
        condition: on-failure
    ports:
      # 设置对外端口
      - "8388:8388/tcp"
      - "8388:8388/udp"
    environment:
      # 密码
      - PASSWORD=9MLSpPmNt
    networks:
      - webnet
networks:
  webnet:
```
:warning: 注意修改端口号和密码


**初始化集群管理**
```
$ docker swarm init --advertise-addr <ip|interface>[:port] --listen-addr <ip|interface>[:port]
```
`<ip|interface>[:port]` 替换为你的本地ip地址，如： `10.10.10.10:8888`

**启动镜像**
```
docker stack deploy -c docker-compose.yml ss_server
```

**查看运行的容器**

```
docker stack ps ss_server
```
