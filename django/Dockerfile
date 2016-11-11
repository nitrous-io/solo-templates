FROM nitrous/python:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# postgresql-9.5          9.5.5-1.pgdg14.04+1
# postgresql-contrib-9.5  9.5.5-1.pgdg14.04+1
#
# requirements.txt:
# django        1.8.5
# gunicorn      19.3.0
# ipython       4.0.0
# psycopg2      2.6.1

# set up postgres
RUN \
  echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -sc)-pgdg main" | tee /etc/apt/sources.list.d/postgresql.list && \
  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
  apt-get update && \
  apt-get install -y \
    postgresql-9.5=9.5.5-1.pgdg14.04+1 \
    postgresql-contrib-9.5=9.5.5-1.pgdg14.04+1 \
    libpq-dev && \
  apt-get clean

COPY support/pg_hba.conf /etc/postgresql/9.5/main/pg_hba.conf

RUN service postgresql start && \
  su postgres -c 'createdb example_development && \
  createuser --superuser $NITROUS_USERNAME' && \
  service postgresql stop

COPY support/install-app /tmp/install-app

COPY support/requirements.txt /tmp/requirements.txt

USER $NITROUS_USERNAME

RUN /bin/bash -l -c 'sudo service postgresql start && \
  /tmp/install-app && \
  sudo service postgresql stop'

USER root
