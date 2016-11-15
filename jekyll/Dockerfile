FROM nitrous/ruby:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# jekyll 3.1.3

USER $NITROUS_USERNAME

RUN /bin/bash -l -c \
  'gem install jekyll -v 3.1.3'

RUN /bin/bash -l -c \
  'cd /home/$NITROUS_USERNAME/code && \
  jekyll new jekyll && \
  echo -e "\nhost: 0.0.0.0\nport: 4000\n" >> /home/$NITROUS_USERNAME/code/jekyll/_config.yml'

USER root
