FROM nitrous/ruby:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-05-11
# rails                   4.2.6
# postgresql-9.5          9.5.5-1.pgdg14.04+1
# postgresql-contrib-9.5  9.5.5-1.pgdg14.04+1
# heroku-toolbelt         3.42.25 (inherited from nitrous/nodejs)

# set up postgres
USER root
RUN \
  echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -sc)-pgdg main" | tee /etc/apt/sources.list.d/postgresql.list && \
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
  apt-get update && \
  apt-get install -y \
    postgresql-9.5=9.5.5-1.pgdg14.04+1 \
    postgresql-contrib-9.5=9.5.5-1.pgdg14.04+1 \
    libpq-dev \
    sqlite3 \
    libsqlite3-dev && \
  apt-get clean

COPY files/pg_hba.conf /etc/postgresql/9.5/main/pg_hba.conf

RUN service postgresql start && \
  su postgres -c 'createdb example_development && \
  createuser --superuser $NITROUS_USERNAME' && \
  service postgresql stop

USER $NITROUS_USERNAME

# set up example app
RUN /bin/bash -l -c 'sudo service postgresql start && \
  gem install rails -v 4.2.6 && \
  rbenv rehash && \
  cd /home/$NITROUS_USERNAME/code && \
  rails new example -d postgresql -B && \
  cd example && \
  bundle install && \
  rake db:create db:migrate && \
  sudo service postgresql stop'

USER root
