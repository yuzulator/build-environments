FROM debian:bullseye-slim
LABEL maintainer="yuzuemu"

ENV DEBIAN_FRONTEND=noninteractive
ENV CMAKE_VER=3.22.6

RUN apt-get update && \
    apt-get -y full-upgrade
RUN apt-get install -y \
    cmake \
    curl \
    git \
    glslang-tools \
    libavcodec-dev \
    libavfilter-dev \
    libavutil-dev \
    liblz4-dev \
    libopus-dev \
    libqt5opengl5-dev \
    libsdl2-dev \
    libssl-dev \
    libswscale-dev \
    libtool \
    libusb-1.0-0-dev \
    p7zip-full \
    python3-pip \
    qtmultimedia5-dev \
    qttools5-dev \
    qttools5-dev-tools \
    unzip \
    zip
RUN curl -O -L https://github.com/transifex/cli/releases/latest/download/tx-linux-amd64.tar.gz && \
    tar xf tx-linux-amd64.tar.gz tx && \
    mv tx /usr/bin/tx && \
    rm tx-linux-amd64.tar.gz

# Install CMake from upstream
RUN cd /tmp && \
    curl -OL https://github.com/Kitware/CMake/releases/download/v${CMAKE_VER}/cmake-${CMAKE_VER}-linux-x86_64.tar.gz && \
    tar xvf cmake-${CMAKE_VER}-linux-x86_64.tar.gz && \
    cp -rv cmake-${CMAKE_VER}-linux-x86_64/* /usr && \
    rm -rf cmake-*
