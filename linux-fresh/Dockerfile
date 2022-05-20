FROM ubuntu:18.04
LABEL maintainer="yuzu"

ENV CLANG_VER=14
ENV CMAKE_VER=3.16.9
ENV DEBIAN_FRONTEND=noninteractive
ENV GCC_VER=11
ENV QT_PKG_VER=515
ENV QT_VER=5.15.2
ENV UBUNTU_VER=bionic

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
    pkg-config \
    python3-pip \
    python3-setuptools \
    software-properties-common \
    unzip \
    wget \
    zlib1g-dev \
    zsync && \
    pip3 install conan && \
# Install updated versions of FFmpeg, GCC, Qt, and SDL2 from launchpad repositories
    add-apt-repository -y ppa:beineri/opt-qt-${QT_VER}-${UBUNTU_VER} && \
    add-apt-repository -y ppa:savoury1/graphics && \
    add-apt-repository -y ppa:savoury1/multimedia && \
    add-apt-repository -y ppa:savoury1/ffmpeg4 && \
    add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
    add-apt-repository -y ppa:git-core/ppa && \
    apt-get update -y && \
    apt-get install --no-install-recommends -y \
    g++-${GCC_VER} \
    gcc-${GCC_VER} \
    git \
    glslang-dev \
    glslang-tools \
    libhidapi-dev \
    qt${QT_PKG_VER}base \
    qt${QT_PKG_VER}tools \
    qt${QT_PKG_VER}wayland \
    qt${QT_PKG_VER}webengine && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-${GCC_VER} ${GCC_VER} && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-${GCC_VER} ${GCC_VER} && \
# Install clang from apt.llvm.org
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    echo "deb http://apt.llvm.org/${UBUNTU_VER}/ llvm-toolchain-${UBUNTU_VER}-${CLANG_VER} main" >> /etc/apt/sources.list && \
    apt-get update -y && \
    apt-get install --no-install-recommends -y \
    clang-${CLANG_VER} \
    lld-${CLANG_VER} \
    llvm-${CLANG_VER} \
    llvm-${CLANG_VER}-linker-tools && \
    ln -s $(which clang-${CLANG_VER}) /usr/bin/clang && \
    ln -s $(which clang++-${CLANG_VER}) /usr/bin/clang++ && \
    dpkg-reconfigure ccache && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log

# Install CMake from upstream
# yuzu requires CMake version 3.15, however Ubuntu only provides 3.10 to Bionic.
RUN cd /tmp && \
    wget https://github.com/Kitware/CMake/releases/download/v${CMAKE_VER}/cmake-${CMAKE_VER}-Linux-x86_64.tar.gz && \
    tar xvf cmake-${CMAKE_VER}-Linux-x86_64.tar.gz && \
    cp -rv cmake-${CMAKE_VER}-Linux-x86_64/* /usr && \
    rm -rf cmake-*

# Install Boost 1.75.0 from yuzu-emu/ext-linux-bin
RUN cd /tmp && \
    wget https://github.com/yuzu-emu/ext-linux-bin/raw/main/boost/boost_1_75_0.tar.xz &&\
    tar xvf boost_1_75_0.tar.xz && \
    chown -R root:root boost_1_75_0/ && \
    cp -rv boost_1_75_0/include boost_1_75_0/lib /usr && \
    rm -rf boost*
    
# Setup paths for Qt binaries
ENV LD_LIBRARY_PATH=/opt/qt${QT_PKG_VER}/lib:${LD_LIBRARY_PATH}
ENV PATH=/opt/qt${QT_PKG_VER}/bin:${PATH}

# Fix GCC 11 <-> Qt 5.15 issue
COPY qtconcurrentthreadengine.patch /opt/qt515/qtconcurrentthreadengine.patch
RUN patch /opt/qt515/include/QtConcurrent/qtconcurrentthreadengine.h /opt/qt515/qtconcurrentthreadengine.patch && \
    rm /opt/qt515/qtconcurrentthreadengine.patch

USER 1027
COPY --chown=yuzu:yuzu settings.yml /home/yuzu/.conan/settings.yml
