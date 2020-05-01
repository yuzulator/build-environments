FROM ubuntu:20.04
MAINTAINER yuzu
RUN useradd -m -s /bin/bash yuzu && \
    DEBIAN_FRONTEND=noninteractive apt-get update && apt-get -y full-upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    build-essential \
    libsdl2-dev \
    libssl-dev \
    python \
    qtbase5-dev \
    qtbase5-private-dev \
    qtwebengine5-dev \
    libqt5opengl5-dev \
    wget \
    git \
    ccache \
    cmake \
    ninja-build && \
    apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
