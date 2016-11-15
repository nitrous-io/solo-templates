FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# python3.4-dev       3.4.3-1ubuntu1~14.04.3
# python2.7-dev       2.7.6-8ubuntu0.2
# python-virtualenv   1.11.4-1ubuntu1
# virtualenvwrapper   4.1.1-1

RUN \
  apt-get update && \
  apt-get install -yy \
    python3.4-dev=3.4.3-1ubuntu1~14.04.4 \
    python2.7-dev=2.7.6-8ubuntu0.2 \
    python-virtualenv=1.11.4-1ubuntu1 \
    virtualenvwrapper=4.1.1-1 && \
  apt-get clean && \
  echo 'source /etc/bash_completion.d/virtualenvwrapper' >> /etc/zsh/zprofile
