FROM node:7-alpine

LABEL maintainer "tyzl931019@gmail.com"

RUN npm i -g python \
    && npm i -g shadowsocks-manager

ENTRYPOINT ["/usr/local/bin/ssmgr"]
    


