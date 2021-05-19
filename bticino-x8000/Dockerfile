ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:9.2.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# hadolint ignore=DL3003
RUN \
    apk add --no-cache --virtual .build-dependencies \
           bash \
#           tzdata \
           python3=3.8.10 \
           py3-pip=20.3.4-r0\ 
#           git \
#           openssl 
#           curl 
           mosquitto-clients=1.6.12-r2
           
COPY bticino.py /hassio_bticino_smarter
COPY run.sh /hassio_bticino_smarter
COPY requirements.txt /hassio_bticino_smarter
RUN mkdir /hassio_bticino_smarter/config
COPY config/config.yml /hassio_bticino_smarter/config
COPY config/mqtt_config.yml /hassio_bticino_smarter/config
COPY config/smarter.json /hassio_bticino_smarter/config
RUN mkdir /hassio_bticino_smarter/templates
COPY templates/file_conf.html /hassio_bticino_smarter/templates
COPY templates/index.html /hassio_bticino_smarter/templates
COPY templates/info.html /hassio_bticino_smarter/templates
COPY templates/package.yml.jinja2 /hassio_bticino_smarter/templates

RUN chmod a+x /hassio_bticino_smarter/run.sh

RUN pip3 install -r requirements.txt

CMD [ "/hassio_bticino_smarter/run.sh" ]
