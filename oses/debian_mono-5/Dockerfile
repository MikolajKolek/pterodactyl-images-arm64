FROM    mono:5-slim

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