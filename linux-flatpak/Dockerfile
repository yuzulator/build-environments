FROM ubuntu:20.04
MAINTAINER yuzu

RUN useradd -m -s /bin/bash yuzu && DEBIAN_FRONTEND=noninteractive apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get -y full-upgrade \
    && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
        flatpak flatpak-builder \
        librsvg2-common \
        ca-certificates build-essential libsdl2-dev libssl-dev \
        python qtbase5-dev qtwebengine5-dev libqt5opengl5-dev \
        wget git ccache cmake \
        ninja-build dnsutils gnupg2 \
        sshfs fuse elfutils \
    && rm -Rf /var/lib/apt/lists/* \
    && flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo \
    && flatpak install -v -y flathub org.kde.Platform//5.13 org.kde.Sdk//5.13
