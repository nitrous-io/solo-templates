FROM nitrous/php-apache:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# Create database.
RUN /bin/bash -l -c 'service mysql start && \
  mysql -u nitrous -e "CREATE DATABASE wordpress DEFAULT CHARACTER SET = utf8;" && \
  service mysql stop'

USER $NITROUS_USERNAME

# Setup WordPress.
RUN \
  /bin/bash -c \
    'cd /home/$NITROUS_USERNAME && \
    wget https://wordpress.org/wordpress-4.5.1.tar.gz && \
    tar xvzf wordpress-4.5.1.tar.gz && \
    mv wordpress/* /home/$NITROUS_USERNAME/code/public_html/ && \
    rm -rf wordpress wordpress-4.5.1.tar.gz'

RUN \
  sed -i "s|_x( 'username'|_x( 'nitrous'|g" /home/$NITROUS_USERNAME/code/public_html/wp-admin/setup-config.php && \
  sed -i "s|_x( 'password'|_x( ''|g" /home/$NITROUS_USERNAME/code/public_html/wp-admin/setup-config.php

USER root

# Give Apache user ownership to perform upgrades, install plugins/themes.
# Add Nitrous user to www-data group so it has permissions to edit files.
RUN /bin/bash -c \
  'cd /home/$NITROUS_USERNAME/code/public_html && \
  chown -R www-data:www-data ./* && \
  find . -type d -exec chmod g+rwx {} \; && \
  find . -type f -exec chmod g+rw {} \; && \
  usermod -a -G www-data $NITROUS_USERNAME'
