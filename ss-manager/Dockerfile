FROM node:7-alpine

LABEL maintainer "tyzl931019@gmail.com"

WORKDIR /app

ADD . /app

RUN npm i -g pm2 \
    && npm i -g python \
    && npm i -g shadowsocks-manager

EXPOSE 80 
EXPOSE 4001
EXPOSE 4000
    
CMD pm2 --name "ss" -f start ssmgr -x -- -c /app/ss.yml \
    && ssmgr -c /app/webgui.yml

