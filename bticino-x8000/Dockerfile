ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:9.2.0
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

RUN mkdir /hassiox8000
\
WORKDIR /hassiox8000

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Setup base
# hadolint ignore=DL3003
RUN \
    apk add --no-cache --virtual .build-dependencies \
           bash \
#           tzdata \
           python3==3.8.10 
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
        Flask-HTTPAuth==3.3.0

RUN chmod a+x /hassiox8000/run.sh

#RUN pip3 install -r requirements.txt

CMD [ "/hassiox8000/run.sh" ]
