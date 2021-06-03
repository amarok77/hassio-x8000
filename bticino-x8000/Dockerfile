ARG BUILD_FROM=ghcr.io/hassio-addons/base-python/amd64:6.0.0

# hadolint ignore=DL3006
FROM ${BUILD_FROM}

RUN mkdir /hassiox8000
\
RUN chmod a+rw /hassiox8000
\
WORKDIR /hassiox8000

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# hadolint ignore=DL3003
FROM alpine:latest
\
#RUN apt-get update
\
RUN \
    apk add --no-cache --virtual .build-dependencies \
#    apt-get install \
    \
        bash \
        python3 
#        -y
#           tzdata \
#           python3==3.8.10 
#           py3-pip=20.3.4-r0\ 
#           git \
#           openssl 
#           curl 
#           mosquitto-clients=1.6.12-r2
           
COPY bticino.py /hassiox8000
COPY run.sh /hassiox8000
COPY requirements.txt /hassiox8000
RUN mkdir /hassiox8000/config
COPY config/config.yml /hassiox8000/config
COPY config/mqtt_config.yml /hassiox8000/config
COPY config/smarter.json /hassiox8000/config
RUN mkdir /hassiox8000/templates
COPY templates/file_conf.html /hassiox8000/templates
COPY templates/index.html /hassiox8000/templates
COPY templates/info.html /hassiox8000/templates
COPY templates/package.yml.jinja2 /hassiox8000/templates

RUN \
    apk add --no-cache --virtual .build-dependencies \
        \
        Flask==1.1.1 \
        requests==2.23.0 \
        PyYAML==5.4 \
        apscheduler==3.6.3 \
        paho-mqtt==1.5.0 \
#        python3==3.9.5-r1 \
        Flask-HTTPAuth==3.3.0

RUN chmod a+x /hassiox8000/run.sh

#RUN pip3 install -r requirements.txt


# Copy root filesystem
COPY rootfs /

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
    maintainer="Amarok <caltaste@gmail.com>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Amarok <caltaste@gmail.com>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}


CMD [ "/hassiox8000/run.sh" ]
