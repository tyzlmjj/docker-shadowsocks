# docker-shadowsocks

shadowsocks 容器化，方便部署

## 安装 docker

```
$ curl -sSL https://get.docker.com/ | sh
$ docker --version
```

## 运行SS服务

**直接运行镜像**

```bash
$ docker run -d -e PASSWORD=9MLSpPmNt -p 8388:8388/tcp -p 8388:8388/udp --restart always tyzlmjj/shadowsocks:manager
$ docker ps
```

**或者使用docker-compose运行**

创建一个 `docker-compose.yml` 文件.

```yaml
server:
  image: tyzlmjj/shadowsocks:libev
  ports:
    # 设置对外接口
    - "8388:8388/tcp"
    - "8388:8388/udp"
  environment:
    # 密码
    - PASSWORD=9MLSpPmNt
  restart: always
```

运行ss服务
```
$ docker-compose up -d
```
