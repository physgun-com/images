FROM --platform=$TARGETOS/$TARGETARCH debian:stable-slim

LABEL author="jackk" maintainer="jackk@hyplex.gg"

LABEL org.opencontainers.image.source="https://github.com/hyplexgg/images"
LABEL org.opencontainers.image.license="MIT"

ENV DEBIAN_FRONTEND=noninteractive

RUN dpkg --add-architecture i386 \
        && apt update \
        && apt upgrade -y \
        && apt install -y tar curl gcc g++ lib32gcc-s1 git \
                          libgcc1 libcurl4-gnutls-dev:i386 \
                          libssl1.1:i386 libcurl4:i386 lib32tinfo6 \
                          libtinfo6:i386 lib32z1 lib32stdc++6 \
                          libncurses5:i386 libcurl3-gnutls:i386 \
                          libsdl2-2.0-0:i386 iproute2 gdb libsdl1.2debian \
                          libfontconfig1 telnet net-tools netcat tzdata \
        && useradd -m -d /home/container container

RUN git config --global init.defaultBranch main \
        && git config --global pull.rebase false

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

COPY ./entrypoint.sh /entrypoint.sh

CMD ["/bin/bash", "/entrypoint.sh"]