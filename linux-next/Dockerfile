FROM ubuntu:20.04
LABEL maintainer="yuzu"

ENV CLANG_VER=13
ENV CMAKE_VER=3.16.3
ENV DEBIAN_FRONTEND=noninteractive
ENV GCC_VER=11
ENV QT_VER=5.15.2
ENV UBUNTU_VER=focal
ENV UBUNTU_NEXT=jammy

RUN apt-get update && apt-get -y full-upgrade && apt-get update && apt-get install -y packagekit

RUN echo "APT::Default-Release \"${UBUNTU_VER}\";" >> /etc/apt/apt.conf.d/01-ubuntu

RUN echo "deb http://archive.ubuntu.com/ubuntu ${UBUNTU_NEXT} main restricted universe multiverse" >> "\n" \
    >> /etc/apt/sources.list

RUN apt-get update && apt-get install -y -t jammy gcc-11 g++-11

# Create a user account yuzu (UID 1027) that the container will run as
RUN useradd -m -u 1027 -s /bin/bash yuzu && \
    apt-get install --allow-downgrades -y -t focal \
    autoconf \
    automake \
    build-essential \
    ccache \
    cmake \
    file \
    gpg-agent \
    libxau6=1:1.0.9-0ubuntu1 \
    libxdmcp6=1:1.1.3-0ubuntu1 \
    libxau-dev \
    libxdmcp-dev \
    libxcb1=1.14-2 \
    libxcb1-dev \
    libx11-xcb1 \
    liblz4-dev \
    libopus-dev \
    libssl-dev \
    libtool \
    libusb-1.0-0-dev \
    libzip-dev \
    libzstd-dev \
    nasm \
    ninja-build \
    python3-pip \
    python3-setuptools \
    software-properties-common \
    unzip \
    vim \
    wget \
    zlib1g-dev \
    zsync && \
    # Install updated versions of FFmpeg, GCC, Qt, and SDL2 from launchpad repositories
    add-apt-repository -y ppa:savoury1/ffmpeg4 && \
    add-apt-repository -y ppa:savoury1/multimedia && \
    add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
    add-apt-repository -y ppa:git-core/ppa && \
    apt-get update -y && \
    apt-get install -y -t focal \
    git \
    libgl1 \
    libglx-dev \
    libegl1 \
    libegl-mesa0 \
    libglx0 \
    libglx-mesa0 \
    libgl-dev \
    libx11-6 \
    libx11-dev \
    libx11-dev \
    libxext6 \
    libxext-dev \
    libegl-dev \
    libgl-dev \
    libglvnd-dev \
    libegl1-mesa-dev \
    libgl1-mesa-dev \
    libavcodec-dev \
    libavutil-dev \
    libsdl2-dev \
    libswscale-dev \
    glslang-tools \
    glslang-dev \
    libhidapi-dev && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-${GCC_VER} ${GCC_VER} && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-${GCC_VER} ${GCC_VER} && \
    # Install clang from apt.llvm.org
    wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    echo "deb http://apt.llvm.org/${UBUNTU_NEXT}/ llvm-toolchain-${UBUNTU_NEXT}-${CLANG_VER} main" >> "\n" >> /etc/apt/sources.list && \
    apt-get update -y && \
    apt-get install -y -t jammy \
    clang-${CLANG_VER} python3-pip && \
    ln -s $(which clang-${CLANG_VER}) /usr/bin/clang && \
    ln -s $(which clang++-${CLANG_VER}) /usr/bin/clang++ && \
    dpkg-reconfigure ccache && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
RUN pip3 install conan
# Install Boost 1.75.0 from yuzu-emu/ext-linux-bin
RUN cd /tmp && \
    wget https://github.com/yuzu-emu/ext-linux-bin/raw/main/boost/boost_1_75_0.tar.xz &&\
    tar xvf boost_1_75_0.tar.xz && \
    chown -R root:root boost_1_75_0/ && \
    cp -rv boost_1_75_0/include boost_1_75_0/lib /usr && \
    rm -rf boost*
# Install qt5.15.2 from yuzu-emu/ext-linux-bin
RUN mkdir /usr/local/Qt5
RUN cd /tmp && \
    wget https://github.com/yuzu-emu/ext-linux-bin/raw/main/qt/qt5_5_15_2.tar.xz &&\
    tar xvf qt5_5_15_2.tar.xz && \
    chown -R root:root qt5_5_15_2/ && \
    cp -avR qt5_5_15_2/* /usr/local/Qt5/ && \
    rm -rf qt*
# Setup paths for Qt binaries
ENV LD_LIBRARY_PATH=/usr/local/Qt5/lib:${LD_LIBRARY_PATH}
ENV PATH=/usr/local/Qt5/bin:${PATH}
USER 1027
COPY --chown=yuzu:yuzu settings.yml /home/yuzu/.conan/settings.yml