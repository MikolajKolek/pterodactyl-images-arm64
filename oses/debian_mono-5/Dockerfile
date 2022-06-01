FROM    mono:5-slim

ADD     http://security.debian.org/debian-security/pool/updates/main/c/curl/libcurl3-gnutls_7.52.1-5+deb9u16_arm64.deb libcurl3.deb
ADD     http://security.debian.org/debian-security/pool/updates/main/a/apt/apt-transport-https_1.4.11_arm64.deb apt-transport-https.deb
RUN     dpkg -i libcurl3.deb
RUN     dpkg -i apt-transport-https.deb

RUN     cd /usr/lib/apt/methods
RUN     ln -s http https

RUN     apt-get -y update && apt-get install -y apt-transport-https
RUN     apt-get -y update \
        && apt-get -y upgrade

RUN     apt update -y \
        && apt install -y apt-transport-https ca-certificates curl \
        && apt install -y iproute2 \
        && useradd -d /home/container -m container

USER    container
ENV     USER=container HOME=/home/container
WORKDIR /home/container

COPY    ./entrypoint.sh /entrypoint.sh
CMD     ["/bin/bash", "/entrypoint.sh"]
