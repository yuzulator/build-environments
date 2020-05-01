FROM alpine
MAINTAINER yuzu
RUN adduser -u 1000 -D -s /bin/bash yuzu && \
    apk update && apk add build-base && \
    cmake \
    python3-dev \
    qt5-qttools-dev \
    qt5-qtmultimedia-dev && \
    pip3 install transifex-client && \
    apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log/
