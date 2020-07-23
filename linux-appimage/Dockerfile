FROM ubuntu:18.04
MAINTAINER quriouspixel

ENV QTVER=5.14.2
ENV QTVERMIN=514
ENV LLVMVER=10
ENV GCCVER=10

ENV CLANG_BINARY=clang-${LLVMVER}
ENV CLANGXX_BINARY=clang++-${LLVMVER}
ENV LLD_BINARY=lld-${LLVMVER}
ENV GCC_BINARY=gcc-${GCCVER}
ENV GXX_BINARY=g++-${GCCVER}

# Create a user account yuzu (UID 1027) that the container will run as
RUN useradd -m -u 1027 -s /bin/bash yuzu && \
    apt-get update -y && \
    apt-get install -y curl software-properties-common apt-transport-https && \
    add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
    DEBIAN_FRONTEND=noninteractive apt-get update && apt-get -y full-upgrade && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    build-essential \
    $GCC_BINARY $GXX_BINARY \
    libboost-all-dev \
    liblz4-dev \
    libsdl2-dev \
    libssl-dev \
    libopus-dev \
    libzip-dev \
    libzstd-dev \
    zlib1g-dev \
    python \
    python-pip \
    python-setuptools \
    qtbase5-dev \
    qtbase5-private-dev \
    qttools5-dev \
    qtwebengine5-dev \
    libqt5opengl5-dev \
    wget \
    curl \
    git \
    ccache \
    cmake \
    ninja-build && \
    pip install conan && \
    apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
    
RUN \
	update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-${GCCVER} 10 \
	update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-${GCCVER} 10 \
	gcc --version \
	g++ --version 
    
ENV CMAKEVER=3.18.0
RUN \
	curl -sLO https://cmake.org/files/v${CMAKEVER%.*}/cmake-${CMAKEVER}-Linux-x86_64.sh && \
	sh cmake-${CMAKEVER}-Linux-x86_64.sh --prefix=/usr --skip-license && \
	rm ./cmake*.sh && \
	cmake --version
	
USER 1027
RUN conan install catch2/2.11.0@ -s compiler.libcxx=libstdc++11 --build=missing && \
    conan install fmt/6.2.0@ -s compiler.libcxx=libstdc++11 --build=missing && \
    conan install nlohmann_json/3.7.3@ -s compiler.libcxx=libstdc++11 --build=missing

