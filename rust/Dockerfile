FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# multirust 0.8.0
# rust      1.8.0

RUN \
  mkdir -p /usr/local/opt/multirust && \
  chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /usr/local/opt/multirust

USER $NITROUS_USERNAME

RUN \
  /bin/bash -l -c \
    'git clone --recursive https://github.com/brson/multirust /usr/local/opt/multirust && \
    cd /usr/local/opt/multirust && \
    git checkout 0.8.0 && \
    cd /usr/local/opt/multirust/src/rustup && \
    git checkout 18c087f9ca8e2a00227563f10a5ea778eee0ea15 && \
    cd /usr/local/opt/multirust && \
    git config user.email "Nitrous, Inc" && \
    git config user.name "eng@nitrous.io" && \
    git commit -a -m "apply patch Fix bashism" && \
    ./build.sh && \
    sudo ./install.sh && \
    cd && \
    SHELL=/bin/bash multirust default 1.8.0'

USER root
