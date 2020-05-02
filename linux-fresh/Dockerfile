FROM ubuntu:20.04
MAINTAINER yuzu
RUN useradd -m -s /bin/bash yuzu && \
    DEBIAN_FRONTEND=noninteractive apt-get update && apt-get -y full-upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    build-essential \
    libboost-all-dev \
    libsdl2-dev \
    libssl-dev \
    libopus-dev \
    libzstd-dev \
    python \
    python3-pip \
    qtbase5-dev \
    qtbase5-private-dev \
    qtwebengine5-dev \
    libqt5opengl5-dev \
    liblz4-dev \
    zlib1g-dev \
    wget \
    git \
    ccache \
    cmake \
    ninja-build && \
    pip3 install conan && \
    apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
USER yuzu
RUN conan install catch2/2.11.0@ && \
    conan install fmt/6.2.0@ && \
    conan install nlohmann_json/3.7.3@
