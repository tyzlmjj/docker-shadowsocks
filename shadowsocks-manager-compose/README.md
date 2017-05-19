
# shadowsocks-libev + shadowsocks-manager

使用 [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev) 和 [shadowsocks-manager](https://github.com/shadowsocks/shadowsocks-manager) 实现shadowsocks的管理。

这里将他们容器化，并用docker-compose文件启动。

## 使用

复制这个目录文件,然后修改 `ss.yml` 和 `webgui.yml` 文件中的内容。如果需要修改端口号，需要同时修改`.env`文件.

执行以下命令启动

```shell
docker-compose -f shadowsocks-manager-compose.yml -p shadowsocks_manager up -d
```
