FROM        --platform=$BUILDPLATFORM ghcr.io/mikolajkolek/images:debian

ENV         DEBIAN_FRONTEND noninteractive

RUN         apt-get update -y \
            && apt-get upgrade -y \
            && apt-get install -y apt-transport-https wget iproute2 \
            && wget https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
            && dpkg -i packages-microsoft-prod.deb \
            && rm packages-microsoft-prod.deb \
            && apt-get update -y \
            && apt-get install -y libgdiplus libgssapi-krb5-2 libssl1.1 libstdc++6 zlib1g

RUN         wget https://dot.net/v1/dotnet-install.sh \ 
            && chmod +x dotnet-install.sh \
            && mkdir -p /dotnet \
            && ./dotnet-install.sh -c 5.0 -InstallDir /dotnet

ENV         DOTNET_ROOT="/dotnet" 
ENV         PATH="/dotnet:${PATH}"

USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container

COPY        ./../entrypoint.sh /entrypoint.sh
CMD         [ "/bin/bash", "/entrypoint.sh" ]
