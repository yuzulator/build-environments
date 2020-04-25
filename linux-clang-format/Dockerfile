FROM ubuntu:20.04
MAINTAINER yuzu
RUN useradd -m -s /bin/bash yuzu
RUN apt-get update && apt-get -y full-upgrade
RUN apt-get install -y git clang-format-6.0

# cleanup all extra information that apt may be caching to save storage space
RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/
