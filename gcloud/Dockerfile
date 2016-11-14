FROM nitrous/ubuntu:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# 2015-02-17
# cloud-sdk-docker d51ef2e632e5877bb123333bee56062fce35d678
# https://github.com/GoogleCloudPlatform/cloud-sdk-docker

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive && apt-get install -y -qq --no-install-recommends \
    wget unzip python php5-mysql php5-cli php5-cgi openjdk-7-jre-headless \
    openssh-client python-openssl && \
  apt-get clean

ENV CLOUDSDK_PYTHON_SITEPACKAGES 1

USER $NITROUS_USERNAME

RUN \
  cd /home/$NITROUS_USERNAME && \
  wget https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.zip -O google-cloud-sdk-0.9.69.zip && \
  unzip google-cloud-sdk-0.9.69.zip -d /home/$NITROUS_USERNAME/ && \
  rm google-cloud-sdk-0.9.69.zip

RUN \
  cd /home/$NITROUS_USERNAME/google-cloud-sdk && \
  ./install.sh --usage-reporting=true

# setup rc files
RUN \
  /bin/bash -l -c \
    'echo -e "\n# Google Cloud SDK\nsource \"/home/$NITROUS_USERNAME/google-cloud-sdk/path.zsh.inc\"\nsource \"/home/$NITROUS_USERNAME/google-cloud-sdk/completion.zsh.inc\"" >> /home/$NITROUS_USERNAME/.zshrc && \
    echo -e "\n# Google Cloud SDK\nsource \"/home/$NITROUS_USERNAME/google-cloud-sdk/path.bash.inc\"\nsource \"/home/$NITROUS_USERNAME/google-cloud-sdk/completion.bash.inc\"" >> /home/$NITROUS_USERNAME/.bashrc'

RUN \
  cd /home/$NITROUS_USERNAME/google-cloud-sdk && \
  yes | ./bin/gcloud components update app-engine-java app-engine-python preview app --allow-no-backup

USER root
