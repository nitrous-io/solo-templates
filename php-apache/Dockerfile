FROM nitrous/php:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-05-27
# apache2               2.4.7-1ubuntu4.13
# libapache2-mod-php7   7.0.13-1+deb.sury.org~trusty+1

# install apache

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install \
    apache2=2.4.7-1ubuntu4.13 \
    libapache2-mod-php7.0=7.0.13-1+deb.sury.org~trusty+1 && \
  apt-get clean

RUN \
  /bin/bash -c \
    'mkdir /home/$NITROUS_USERNAME/code/public_html && \
    echo "<?php phpinfo(); ?>" > /home/$NITROUS_USERNAME/code/public_html/index.php && \
    chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /home/$NITROUS_USERNAME/code/public_html && \
    chmod 775 /home/$NITROUS_USERNAME/code/public_html' && \
    chown -R $NITROUS_USERNAME:www-data /home/$NITROUS_USERNAME/code/public_html

RUN \
  sed -i 's|variables_order.*|variables_order = "EGPCS"|g' /etc/php/7.0/apache2/php.ini && \
  sed -i 's|upload_max_filesize.*|upload_max_filesize = 100M|g' /etc/php/7.0/apache2/php.ini && \
  sed -i 's|post_max_size.*|post_max_size = 100M|g' /etc/php/7.0/apache2/php.ini && \
  sed -i 's|;cgi.fix_pathinfo=1|cgi.fix_pathinfo=0|g' /etc/php/7.0/apache2/php.ini && \
  sed -i 's|Listen 80|Listen 3000|g' /etc/apache2/ports.conf && \
  sed -i 's|VirtualHost \*:80|VirtualHost *:3000|g' /etc/apache2/sites-available/000-default.conf && \
  sed -i "s|/var/www/html|/home/${NITROUS_USERNAME}/code/public_html|g" /etc/apache2/sites-available/000-default.conf && \
  echo "<Directory /home/${NITROUS_USERNAME}/code/public_html>\n\
    Options Indexes FollowSymLinks\n\
    AllowOverride None\n\
    Require all granted\n\
  </Directory>\n"\
  >> /etc/apache2/apache2.conf
