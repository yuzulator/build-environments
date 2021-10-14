FROM debian:bullseye-slim
LABEL maintainer="yuzuemu"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get -y full-upgrade
RUN apt-get install -y git p7zip-full libqt5opengl5-dev qtmultimedia5-dev qttools5-dev qttools5-dev-tools \
    python3-pip cmake libavcodec-dev libavutil-dev libsdl2-dev libswscale-dev liblz4-dev libopus-dev \
    libssl-dev libtool libusb-1.0-0-dev glslang-tools
RUN pip3 install transifex-client conan
