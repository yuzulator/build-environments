FROM ubuntu:20.04
MAINTAINER yuzu
RUN useradd -m -s /bin/bash yuzu && \
    apt-get update && apt-get -y full-upgrade && \
    apt-get install -y git clang-format-6.0 && \
    apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
