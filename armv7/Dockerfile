FROM nginx:1.12.2

MAINTAINER Emanuel Freitas "ejsfreitas@gmail.com"

WORKDIR /root

ENV DOCKER_GEN_VERSION 0.7.3

ADD https://github.com/just-containers/s6-overlay/releases/download/v1.21.2.1/s6-overlay-armhf.tar.gz /tmp/
ADD https://github.com/jwilder/docker-gen/releases/download/0.7.3/docker-gen-linux-armhf-$DOCKER_GEN_VERSION.tar.gz /tmp/

RUN tar xzf /tmp/s6-overlay-armhf.tar.gz -C / &&\
    tar -C /bin -xzf /tmp/docker-gen-linux-armhf-$DOCKER_GEN_VERSION.tar.gz && \
    rm /tmp/docker-gen-linux-armhf-$DOCKER_GEN_VERSION.tar.gz && \
    rm /tmp/s6-overlay-armhf.tar.gz && \
    rm /etc/nginx/conf.d/default.conf && \
    apt-get update && \
    apt-get install -y python ruby cron iproute2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

COPY ./fs_overlay /

RUN chmod a+x /bin/* && \
    chmod a+x /etc/cron.weekly/renew_certs

VOLUME /var/lib/https-portal

ENTRYPOINT ["/init"]
