FROM ubuntu:20.04
MAINTAINER yuzu
RUN useradd -m -s /bin/bash yuzu
RUN DEBIAN_FRONTEND=noninteractive apt-get update && apt-get -y full-upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    build-essential \
    libsdl2-dev \
    libssl-dev \
    python \
    qtbase5-dev \
    qtwebengine5-dev \
    libqt5opengl5-dev \
    wget \
    git \
    ccache \
    cmake \
    ninja-build

# cleanup all extra information that apt may be caching to save storage space
RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/
