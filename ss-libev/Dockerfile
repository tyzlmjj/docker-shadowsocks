FROM alpine

LABEL maintainer "tyzl931019@gmail.com"

ARG SS_VER=3.2.3
ARG SS_URL=https://github.com/shadowsocks/shadowsocks-libev/releases/download/v$SS_VER/shadowsocks-libev-$SS_VER.tar.gz

ENV SERVER_ADDR  0.0.0.0
ENV SERVER_ADDR_IPV6 ::0
ENV SERVER_PORT  8388
ENV PASSWORD     123456
ENV METHOD       aes-256-cfb
ENV TIMEOUT      300
ENV DNS_ADDR     8.8.8.8
ENV DNS_ADDR_2   8.8.4.4

# 设置镜像源为清华的(国内使用)
# RUN sed -i 's/http:\/\/dl-cdn.alpinelinux.org/https:\/\/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories

RUN set -ex && \
    # Build environment setup
    apk add --no-cache --virtual .build-deps \
            curl \
            tar \
            autoconf \
            build-base \
            c-ares-dev \
            libev-dev \
            libtool \
            libsodium-dev \
            linux-headers \
            mbedtls-dev \
            pcre-dev && \
    # Download & install
    cd /tmp && \
    curl -sSL $SS_URL | tar xz --strip 1 && \
    ./configure --prefix=/usr --disable-documentation && \
    make install && \
    cd .. && \
    runDeps="$( \
        scanelf --needed --nobanner /usr/bin/ss-* \
            | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
            | xargs -r apk info --installed \
            | sort -u \
    )" && \
    # Runtime dependencies setup
    apk add --no-cache --virtual .run-deps $runDeps && \
    apk del .build-deps && \
    rm -rf /tmp/*

CMD ss-server -s $SERVER_ADDR \
              -s $SERVER_ADDR_IPV6 \
              -p $SERVER_PORT \
              -k ${PASSWORD:-$(hostname)} \
              -m $METHOD \
              -t $TIMEOUT \
              --fast-open \
              -d $DNS_ADDR \
              -d $DNS_ADDR_2 \
              -u
