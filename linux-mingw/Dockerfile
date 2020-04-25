FROM archlinux:latest
MAINTAINER yuzu
RUN useradd -m -s /bin/bash yuzu && mkdir -p /tmp/pkgs
# Add mingw-repo "ownstuff" is a AUR with an up to date mingw64
RUN echo "[ownstuff]" >> /etc/pacman.conf \
    && echo "SigLevel = Optional TrustAll" >> /etc/pacman.conf \
    && echo "Server = https://martchus.no-ip.biz/repo/arch/ownstuff/os/\$arch" >> /etc/pacman.conf
RUN pacman -Syu --noconfirm
RUN pacman -Syu --noconfirm
RUN pacman -S --needed --noconfirm --noprogressbar \
    base-devel \
    gnupg \
    wget \
    git \
    python-pip \
    python \
    ccache \
    p7zip \
    cmake \
    ninja \
    mingw-w64-gcc \
    mingw-w64-tools \
    mingw-w64-sdl2 \
    mingw-w64-qt5-base \
    mingw-w64-qt5-tools \
    mingw-w64-qt5-graphicaleffects \
    mingw-w64-qt5-multimedia \
    mingw-w64-qt5-winextras \
    python2 \
    mingw-w64-opus \
    mingw-w64-winpthreads

COPY mingw-setup.sh /tmp/pkgs
RUN cd /tmp/pkgs && bash -e mingw-setup.sh
# Compatibility with the old Ubuntu MingW image
RUN ln -s /usr/x86_64-w64-mingw32/lib/qt /usr/x86_64-w64-mingw32/lib/qt5

# Cleanup
USER root
RUN pacman -Scc --noconfirm
RUN rm -rf /usr/share/man/*; \
    rm -rf /tmp/*; \
    rm -rf /var/tmp/*;
