#FROM tutum/curl:trusty
FROM armv7/armhf-ubuntu:xenial
MAINTAINER Janek Thomaschewski <janek_docker@jbbr.net>

# Install curl
RUN apt-get update && apt-get -y install curl && rm -rf /var/lib/apt/lists/*

# Install InfluxDB
ENV INFLUXDB_VERSION 1.1.1

RUN curl -s -o /tmp/influxdb_armhf.tar.gz https://dl.influxdata.com/influxdb/releases/influxdb-${INFLUXDB_VERSION}_linux_armhf.tar.gz && \
  cd /tmp && \
  tar xfvz influxdb_armhf.tar.gz && \
  cp -r influxdb-${INFLUXDB_VERSION}-*/* / && \
  rm -rf influxdb-${INFLUXDB_VERSION}-* influxdb_armhf.tar.gz

ADD types.db /usr/share/collectd/types.db
ADD config.toml /config/config.toml
ADD run.sh /run.sh
RUN chmod +x /*.sh

ENV PRE_CREATE_DB **None**
ENV SSL_SUPPORT **False**
ENV SSL_CERT **None**

# Admin server WebUI
EXPOSE 8083

# HTTP API
EXPOSE 8086

# Raft port (for clustering, don't expose publicly!)
#EXPOSE 8090

# Protobuf port (for clustering, don't expose publicly!)
#EXPOSE 8099

VOLUME ["/data"]

CMD ["/run.sh"]
