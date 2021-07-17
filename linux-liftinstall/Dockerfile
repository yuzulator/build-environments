FROM debian:stable
MAINTAINER yuzu

# Create a user account yuzu (UID 1027) that the container will run as
RUN apt-get update && apt-get -y full-upgrade && \
    apt-get install --no-install-recommends -y \
    ca-certificates \
    curl \
    gnupg \
    apt-utils && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg -o /tmp/pubkey.gpg && \
    apt-key add /tmp/pubkey.gpg && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list && \
    apt-get update && apt-get install --no-install-recommends -y \
    libwebkit2gtk-4.0-dev \
    libssl-dev \
    cargo \
    nodejs \
    yarn && \
    apt-get clean autoclean && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log
