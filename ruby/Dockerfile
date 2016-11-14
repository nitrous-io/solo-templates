FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# ruby              2.3.1 (Default)
# bundler           1.11.2
# heroku-toolbelt   3.42.25 (inherited from nitrous/nodejs)

RUN \
  mkdir -p /usr/local/opt/rbenv && \
  /bin/bash -c 'chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /usr/local/opt/rbenv'

RUN \
  echo 'export RBENV_ROOT=/usr/local/opt/rbenv' >> /etc/profile && \
  echo 'export PATH=$RBENV_ROOT/bin:$PATH' >> /etc/profile && \
  echo 'eval "$($RBENV_ROOT/bin/rbenv init -)"' >> /etc/profile && \
  echo 'export PATH=.bundle/binstubs:$PATH' >> /etc/profile

COPY files/gemrc /home/$NITROUS_USERNAME/.gemrc
COPY files/bundle-config /home/$NITROUS_USERNAME/.bundle/config

RUN \
  /bin/bash -c 'chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /home/$NITROUS_USERNAME/.gemrc /home/$NITROUS_USERNAME/.bundle'

# Needed to compile ruby.
RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yy \
    libreadline-dev

USER $NITROUS_USERNAME

RUN \
  /bin/bash -c \
    'git clone https://github.com/sstephenson/rbenv.git /usr/local/opt/rbenv && \
    git clone https://github.com/sstephenson/ruby-build.git /usr/local/opt/rbenv/plugins/ruby-build'

RUN \
  /bin/bash -l -c \
    'rbenv install 2.3.1 && \
    rbenv global 2.3.1 && \
    rbenv rehash && \
    ruby -v && \
    gem install bundler --version=1.11.2 && \
    rbenv rehash'

USER root
