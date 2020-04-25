FROM alpine
RUN adduser -u 1000 -D -s /bin/bash yuzu
RUN apk update && apk add build-base cmake python3-dev qt5-qttools-dev qt5-qtmultimedia-dev
RUN pip3 install transifex-client

# cleanup all extra information that apt may be caching to save storage space
RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/
