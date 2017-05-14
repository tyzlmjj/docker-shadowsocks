FROM ubuntu:16.04
MAINTAINER gyteng <igyteng@gmail.com>
RUN apt-get update && \
    apt-get install curl git sudo -y && \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get install -y nodejs && \
    npm i -g shadowsocks-manager && \
    git clone https://github.com/shadowsocks/shadowsocks-libev.git ~/shadowsocks && \
    mkdir -p ~/build-area/ && \
    cp ~/shadowsocks/scripts/build_deb.sh ~/build-area/ && \
    cd ~/build-area && \
    ./build_deb.sh
ENTRYPOINT ["/usr/bin/ssmgr"]
