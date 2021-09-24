FROM archlinux:latest
MAINTAINER yuzu
# Workaround for Arch Linux Docker image failing to build
# From https://stackoverflow.com/questions/66154574
RUN patched_glibc=glibc-linux4-2.33-4-x86_64.pkg.tar.zst && \
    curl -LO "https://repo.archlinuxcn.org/x86_64/$patched_glibc" && \
    bsdtar -C / -xvf "$patched_glibc" && \
    echo 'IgnorePkg = glibc' >> /etc/pacman.conf
# Add mingw-repo "ownstuff" is a AUR with an up to date mingw64
# Runs pacman -Syu twice in order to work around pacman issues where the first run only updates the current distro packages
# and the second run actually pulls the updates from the repos.
RUN useradd -m -u 1027 -s /bin/bash yuzu && mkdir -p /tmp/pkgs && \
    echo "[ownstuff]" >> /etc/pacman.conf && \
    echo "SigLevel = Optional TrustAll" >> /etc/pacman.conf && \
    echo "Server = https://martchus.no-ip.biz/repo/arch/ownstuff/os/\$arch" >> /etc/pacman.conf && \
    pacman -Syu --noconfirm && \
    pacman -Syu --noconfirm && \
    pacman -S --needed --noconfirm --noprogressbar \
    base-devel \
    gnupg \
    wget \
    git \
    glslang \
    python-pip \
    python \
    ccache \
    p7zip \
    cmake \
    ninja \
    mingw-w64-boost \
    mingw-w64-gcc \
    mingw-w64-lz4 \
    mingw-w64-opus \
    mingw-w64-sdl2 \
    mingw-w64-tools \
    mingw-w64-winpthreads \
    mingw-w64-zlib \
    && \
    cd /tmp && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-fmt-8.0.0-5-any.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-qt5-base-5.15.2-1-x86_64.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-qt5-declarative-5.15.2-1-x86_64.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-qt5-graphicaleffects-5.15.2-1-any.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-qt5-multimedia-5.15.2-1-any.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-qt5-tools-5.15.2-1-x86_64.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-qt5-winextras-5.15.2-1-any.pkg.tar.zst && \
    wget -q https://github.com/yuzu-emu/ext-linux-bin/raw/main/mingw/mingw-w64-zstd-1.5.0-1-any.pkg.tar.zst && \
    pacman -U --noconfirm --noprogressbar mingw-w64-{fmt-8.0.0-5-any,qt5-base-5.15.2-1-x86_64,qt5-declarative-5.15.2-1-x86_64,qt5-graphicaleffects-5.15.2-1-any,qt5-multimedia-5.15.2-1-any,qt5-tools-5.15.2-1-x86_64,qt5-winextras-5.15.2-1-any,zstd-1.5.0-1-any}.pkg.tar.zst && \
    pacman -Scc --noconfirm && \
    rm -rf /usr/share/man/ /tmp/* /var/tmp/ /usr/{i686-w64-mingw32,lib32} /usr/lib/gcc/i686-w64-mingw32

# Setup extra mingw work arounds
RUN pip3 install pefile
# Compatibility with the old Ubuntu MingW image
RUN ln -s /usr/x86_64-w64-mingw32/lib/qt /usr/x86_64-w64-mingw32/lib/qt5

# Install conan and add the mingw cross compile as the default profile
RUN pip3 install conan
COPY --chown=yuzu:yuzu default /home/yuzu/.conan/profiles/
COPY --chown=yuzu:yuzu settings.yml /home/yuzu/.conan/settings.yml
USER 1027
