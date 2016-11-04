FROM nitrous/ubuntu:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# nvm             0.31.0
# node            6.0.0
# npm             3.8.6

RUN \
  mkdir -p /usr/local/opt/nvm && \
  /bin/bash -c 'chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /usr/local/opt/nvm'

RUN echo 'source /usr/local/opt/nvm/nvm.sh' >> /etc/profile

USER $NITROUS_USERNAME

RUN \
  /bin/bash -c \
    'git clone https://github.com/creationix/nvm.git /usr/local/opt/nvm && \
    cd /usr/local/opt/nvm && git checkout v0.31.0 2>/dev/null && \
    source /usr/local/opt/nvm/nvm.sh && \
    nvm install 6.0.0 && \
    nvm alias default 6.0.0 && \
    nvm use 6.0.0 && \
    npm install -g npm@3.8.6'


# set up heroku toolbelt
USER root
RUN /bin/bash -c 'wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh'
USER $NITROUS_USERNAME
RUN /bin/bash -c 'heroku version'

USER root
