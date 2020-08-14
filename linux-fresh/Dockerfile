FROM ubuntu:20.04
MAINTAINER yuzu
# Create a user account yuzu (UID 1027) that the container will run as
RUN useradd -m -u 1027 -s /bin/bash yuzu && \
    DEBIAN_FRONTEND=noninteractive apt-get update && apt-get -y full-upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    build-essential \
    libboost-all-dev \
    liblz4-dev \
    libsdl2-dev \
    libssl-dev \
    libopus-dev \
    libzip-dev \
    libzstd-dev \
    zlib1g-dev \
    python \
    python3-pip \
    qtbase5-dev \
    qtbase5-private-dev \
    qttools5-dev \
    qtwebengine5-dev \
    libqt5opengl5-dev \
    wget \
    git \
    ccache \
    cmake \
    ninja-build && \
    pip3 install conan && \
    apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
USER 1027
RUN conan install catch2/2.13.0@ -s compiler.libcxx=libstdc++11 --build=missing && \
    conan install fmt/7.0.3@ -s compiler.libcxx=libstdc++11 --build=missing && \
    conan install nlohmann_json/3.9.1@ -s compiler.libcxx=libstdc++11 --build=missing
