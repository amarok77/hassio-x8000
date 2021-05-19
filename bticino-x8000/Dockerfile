ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:9.2.0
FROM ${BUILD_FROM}


RUN mkdir /hassio_bticino_smarter
#RUN chmod a=rw /hassio_bticino_smarter
WORKDIR /hassio_bticino_smarter

RUN apk add --no-cache --virtual build-deps \
           bash \
#           tzdata \
#           python3 \
           pip3 
#           git \
#           openssl 
#           curl 
#           mosquitto-clients
           
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
