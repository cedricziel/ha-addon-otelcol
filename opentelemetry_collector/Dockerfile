# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH
RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"

RUN apk add "https://github.com/open-telemetry/opentelemetry-collector-releases/releases/download/v0.52.0/otelcol-contrib_0.52.0_linux_${BUILD_ARCH}.apk"

# Copy root filesystem
COPY rootfs /
