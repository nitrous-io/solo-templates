FROM nitrous/php:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2015-07-14
# laravel-installer   1.1.3
# laravel             4.2
# redis-server        2:2.8.4-2

ENV NITROUS_PREVIEW_PORT 3000

# enable mcrypt in php
RUN php5enmod mcrypt

# create database
RUN /bin/bash -l -c 'service mysql start && \
  mysql -u nitrous -e "CREATE DATABASE laravel DEFAULT CHARACTER SET = utf8;" && \
  service mysql stop'

# install redis
RUN \
  apt-get update && \
  apt-get install -y --no-install-recommends \
    redis-server=2:2.8.4-2 && \
  apt-get clean

USER $NITROUS_USERNAME

# install laravel
RUN /bin/bash -c 'composer global require "laravel/installer=1.1.3"'

# create laravel app
RUN /bin/bash -c 'mkdir -p /home/$NITROUS_USERNAME/code/example && \
  composer create-project laravel/laravel /home/$NITROUS_USERNAME/code/example 4.2 --prefer-dist'

# database configuration
COPY support/database.php /home/$NITROUS_USERNAME/code/example/config/database.php
COPY support/start-app /home/$NITROUS_USERNAME/code/example/start-app

USER root

# set proper ownership
RUN /bin/bash -c 'chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /home/$NITROUS_USERNAME/code/example'
