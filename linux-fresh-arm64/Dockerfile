FROM ubuntu:22.04
LABEL maintainer="yuzu"

ENV CMAKE_VER=3.22.6
ENV DEBIAN_FRONTEND=noninteractive
ENV GCC_VER=11.2.0
ENV QT_PKG_VER=515
ENV QT_VER=5.15.3
ENV UBUNTU_VER=jammy

# Create a user account yuzu (UID 1027) that the container will run as
RUN useradd -m -u 1027 -s /bin/bash yuzu && \
    apt-get update && apt-get -y full-upgrade && \
    apt-get install --no-install-recommends -y \
    appstream \
    autoconf \
    automake \
    build-essential \
    ccache \
    desktop-file-utils \
    file \
    gpg-agent \
    libfile-mimeinfo-perl \
    libglu1-mesa-dev \
    libpulse-dev \
    libssl-dev \
    libtool \
    libudev-dev \
    libva-dev \
    libwayland-dev \
    libzip-dev \
    mesa-common-dev \
    nasm \
    ninja-build \
    patchelf \
    pkg-config \
    software-properties-common \
    unzip \
    wget \
    zlib1g-dev \
    zsync \
# vcpkg requirements
    curl \
    zip \
    && \
    apt-get update -y && \
    apt-get install --no-install-recommends -y \
    cmake \
    git \
    glslang-dev \
    glslang-tools \
    libhidapi-dev \
    qtbase5-dev \
    qtbase5-private-dev \
    qttools5-dev \
    qtwayland5 \
    qtmultimedia5-dev \
    qtwebengine5-dev && \
    dpkg-reconfigure ccache && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log

# Tell CMake to use vcpkg when looking for packages
ENV VCPKG_TOOLCHAIN_FILE=/home/yuzu/vcpkg/scripts/buildsystems/vcpkg.cmake
ENV VCPKG_FORCE_SYSTEM_BINARIES=1

USER 1027
# Install vcpkg and required dependencies for yuzu
RUN cd /home/yuzu &&\
    git clone --depth 1 https://github.com/Microsoft/vcpkg.git &&\
    cd vcpkg &&\
    ./bootstrap-vcpkg.sh &&\
    ./vcpkg install \
        boost-algorithm \
        boost-asio \
        boost-bind \
        boost-config \
        boost-container \
        boost-context \
        boost-crc \
        boost-functional \
        boost-icl \
        boost-intrusive \
        boost-mpl \
        boost-process \
        boost-range \
        boost-spirit \
        boost-test \
        boost-timer \
        boost-variant \
        fmt \
        lz4 \
        nlohmann-json \
        zlib \
        zstd
