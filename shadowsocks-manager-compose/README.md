
# shadowsocks-libev + shadowsocks-manager

使用 [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev) 和 [shadowsocks-manager](https://github.com/shadowsocks/shadowsocks-manager) 实现shadowsocks的管理。

这里将他们容器化，并用docker-compose文件启动。

## 使用

复制这个目录文件。修改[webgui.yml](https://github.com/tyzlmjj/docker-shadowsocks/blob/master/shadowsocks-manager-compose/ssmgr/webgui.yml)里面的一些配置信息。

在这个目录执行以下命令就可以启动

```shell
docker-compose -f shadowsocks-manager-compose.yml -p shadowsocks_manager up -d
```


**需要注意的地方:**
1. 如果需要修改一些端口号，可能需要同时修改[.env](https://github.com/tyzlmjj/docker-shadowsocks/blob/master/shadowsocks-manager-compose/.env)、[webgui.yml](https://github.com/tyzlmjj/docker-shadowsocks/blob/master/shadowsocks-manager-compose/ssmgr/webgui.yml)、[ss.yml](https://github.com/tyzlmjj/docker-shadowsocks/blob/master/shadowsocks-manager-compose/ssmgr/ss.yml)三个文件
2. [webgui.yml](https://github.com/tyzlmjj/docker-shadowsocks/blob/master/shadowsocks-manager-compose/ssmgr/webgui.yml)文件中启用的模块必须全部打开，也就是`use: true`。如果单独关闭一些模块可能会有错误。
3. 我用docker启动了三个容器，默认都使用主机网络，所以配置文件中的IP地址都不需要修改。
