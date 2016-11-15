FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2016-04-28
# meteor          1.3.2.4
# heroku-toolbelt 3.42.25

# Install Meteor.
USER $NITROUS_USERNAME
RUN curl https://install.meteor.com/ | sed 's/RELEASE=.*/RELEASE="1.3.2.4"/' | sh

USER root
