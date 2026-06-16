ARG BUILD_FROM=ghcr.io/home-assistant/amd64-base:3.24
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set Shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup Base
ARG BUILD_ARCH=amd64
ARG DEHYDRATED_VERSION=0.7.2

# hadolint ignore=DL3018
RUN \
    apk add --no-cache \
        openssl \
        jq \
    \
    && curl -s -o /usr/bin/dehydrated \
        "https://raw.githubusercontent.com/dehydrated-io/dehydrated/v${DEHYDRATED_VERSION}/dehydrated" \
    \
    && chmod a+x /usr/bin/dehydrated

# Copy Root Filesystem
COPY rootfs /

# Ensure correct permissions
RUN \
    chmod a+x /etc/s6-overlay/s6-rc.d/ddns-cloudflare/run \
    && chmod a+x /etc/s6-overlay/s6-rc.d/ddns-cloudflare/finish \
    && chmod a+x /usr/bin/ddns-cloudflare-update \
    && chmod a+x /usr/bin/ddns-cloudflare-update-hook

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="MrEditor97 <dev@mreditor97.co.uk>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Add-ons" \
    org.opencontainers.image.authors="MrEditor97 <dev@mreditor97.co.uk>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://github.com/mreditor97/homeassistant-addons" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/master/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
