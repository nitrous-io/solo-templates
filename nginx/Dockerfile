FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-05-13
# nginx     1.10.1-3+trusty2

# install nginx
RUN \
  echo "deb http://ppa.launchpad.net/nginx/stable/ubuntu $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/nginx-stable.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C300EE8C && \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install \
    nginx=1.10.1-3+trusty2 && \
  apt-get clean

# nginx upstart conf scripts are still buggy and doesn't work, use sysvinit instead
RUN \
  rm /etc/init/nginx.conf && \
  update-rc.d nginx defaults

COPY support/nginx-default /etc/nginx/sites-available/default

RUN mkdir -p /home/$NITROUS_USERNAME/public_html

COPY support/index.html /home/$NITROUS_USERNAME/public_html/index.html

RUN chown -R $NITROUS_USERNAME:www-data /home/$NITROUS_USERNAME/public_html
