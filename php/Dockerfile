FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-05-27
# php                   7.0.13-1+deb.sury.org~trusty+1
# mysql-server          5.5.53-0ubuntu0.14.04.1
# libmysqlclient-dev    5.5.53-0ubuntu0.14.04.1
# composer              1.0.0-alpha11

# setup mysql
RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install \
    mysql-server=5.5.53-0ubuntu0.14.04.1 \
    libmysqlclient-dev=5.5.53-0ubuntu0.14.04.1 && \
  apt-get clean

COPY support/setup_mysql tmp/setup_mysql

RUN /bin/bash -l -c 'service mysql start && \
  tmp/setup_mysql && \
  rm tmp/setup_mysql && \
  service mysql stop'

# setup php
RUN apt-get install -y software-properties-common && \
    LC_ALL=C.UTF-8 add-apt-repository -y ppa:ondrej/php

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install \
    php7.0=7.0.13-1+deb.sury.org~trusty+1 \
    php7.0-curl php7.0-gd php7.0-mysql php7.0-mcrypt \
    php5-geoip php7.0-cgi php7.0-dev php7.0-intl \
    php-apc php-pear \
    mcrypt && \
  apt-get clean

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer version=1.0.2
