FROM ubuntu:18.04
MAINTAINER yuzu

RUN useradd -m -s /bin/bash yuzu
RUN apt-get update && apt-get -y full-upgrade && apt-get install --no-install-recommends -y flatpak flatpak-builder ca-certificates
RUN flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
RUN flatpak install -v -y flathub org.kde.Platform//5.13 org.kde.Sdk//5.13
RUN apt-get install --no-install-recommends -y build-essential libsdl2-dev libssl-dev python qtbase5-dev qtwebengine5-dev libqt5opengl5-dev wget git ccache cmake ninja-build dnsutils gnupg2 sshfs fuse elfutils
 
