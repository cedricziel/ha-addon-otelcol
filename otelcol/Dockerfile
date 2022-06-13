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
    OTELCOL="0.52.0" \
    && echo "${BUILD_ARCH}" \
    && ARCH="${BUILD_ARCH}" \
    && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi \
    && curl -J -L -o /tmp/otelcol-contrib.tar.gz "https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v${OTELCOL}/otelcol-contrib_${OTELCOL}_linux_${ARCH}.tar.gz" \
    && tar -xzvf /tmp/otelcol-contrib.tar.gz -C /tmp \
    && mv /tmp/otelcol-contrib /usr/bin/
