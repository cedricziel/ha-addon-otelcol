# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM=ghcr.io/home-assistant/aarch64-base:3.13
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

# Copy root filesystem
COPY rootfs /

RUN \
    OTELCOL="0.53.0" \
    && echo "${BUILD_ARCH}" \
    && ARCH="${BUILD_ARCH}" \
    && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi \
    && curl -J -L -o /tmp/otelcol-contrib.tar.gz "https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v${OTELCOL}/otelcol-contrib_${OTELCOL}_linux_${ARCH}.tar.gz" \
    && tar -xzvf /tmp/otelcol-contrib.tar.gz -C /tmp \
    && mv /tmp/otelcol-contrib /usr/bin/ \
    && chmod +x /usr/bin/otelcol-contrib

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
    maintainer="Cedric Ziel <mail@cedric-ziel.com>" \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant OpenTelemetry Collector AddOn" \
    org.opencontainers.image.authors="Cedric Ziel <mail@cedric-ziel.com>" \
    org.opencontainers.image.licenses="Apache2 License" \
    org.opencontainers.image.url="https://github.com/cedricziel/ha-addon-opentelemetry-collector" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
