FROM nitrous/php:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-07-28
# nginx           1.10.1-3+trusty2
# php             7.0.13-1+deb.sury.org~trusty+1
# php7-fpm        7.0.13-1+deb.sury.org~trusty+1

# install nginx / php-fpm
RUN \
  echo "deb http://ppa.launchpad.net/nginx/stable/ubuntu $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/nginx-stable.list && \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C300EE8C && \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install \
    nginx=1.10.1-3+trusty2 \
    php7.0=7.0.13-1+deb.sury.org~trusty+1 \
    php7.0-fpm=7.0.13-1+deb.sury.org~trusty+1 && \
  apt-get clean

# nginx upstart conf scripts are still buggy and doesn't work, use sysvinit instead
RUN \
  rm /etc/init/nginx.conf && \
  update-rc.d nginx defaults

# setup public_html dir
RUN \
  /bin/bash -c \
    'mkdir /home/$NITROUS_USERNAME/code/public_html && \
    echo "<?php phpinfo(); ?>" > /home/$NITROUS_USERNAME/code/public_html/index.php && \
    chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /home/$NITROUS_USERNAME/code/public_html && \
    chmod 775 /home/$NITROUS_USERNAME/code/public_html' && \
    chown -R $NITROUS_USERNAME:www-data /home/$NITROUS_USERNAME/code/public_html

COPY support/nginx-default /etc/nginx/sites-available/default

RUN \
  sed -i 's|variables_order.*|variables_order = "EGPCS"|g' /etc/php/7.0/fpm/php.ini && \
  sed -i 's|upload_max_filesize.*|upload_max_filesize = 100M|g' /etc/php/7.0/fpm/php.ini && \
  sed -i 's|post_max_size.*|post_max_size = 100M|g' /etc/php/7.0/fpm/php.ini && \
  sed -i 's|;cgi.fix_pathinfo=1|cgi.fix_pathinfo=0|g' /etc/php/7.0/fpm/php.ini && \
  sed -i 's|listen =.*|listen = /var/run/php/php7.0-fpm.sock|g' /etc/php/7.0/fpm/pool.d/www.conf && \
  sed -i "s|root /var/www/html|root /home/${NITROUS_USERNAME}/code/public_html|g" /etc/nginx/sites-available/default
