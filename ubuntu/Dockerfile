FROM ubuntu-upstart:trusty
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

ENV NITROUS_USERNAME nitrous
ENV NITROUS_SSH_ENABLED true

# Disable root password
RUN passwd -l root

# Create nitrous user and give sudo
RUN \
  /bin/bash -c \
    'useradd --create-home -s /bin/bash $NITROUS_USERNAME && \
    adduser $NITROUS_USERNAME sudo && \
    mkdir -p /etc/sudoers.d && \
    echo $NITROUS_USERNAME ALL=NOPASSWD:ALL > /etc/sudoers.d/$NITROUS_USERNAME && \
    chmod 0440 /etc/sudoers.d/$NITROUS_USERNAME'

RUN \
  mkdir -p /nitrous/init /nitrous/initonce && \
  touch /nitrous/dont_delete_this_dir

RUN \
  rm /etc/legal && \
  rm /etc/update-motd.d/10-help-text

COPY files/motd /etc/update-motd.d/00-header
COPY files/nitrous_bootstrap.conf /etc/init/nitrous_bootstrap.conf
COPY files/bootstrap.sh /nitrous/bootstrap.sh
COPY files/dockerenv-inject /nitrous/dockerenv-inject
COPY files/sshd_config /etc/ssh/sshd_config

COPY files/nitrous-unison /nitrous/nitrous-unison
COPY files/nitrous-watcher /nitrous/nitrous-watcher

COPY files/init/0010-inject-env.sh  /nitrous/init/0010-inject-env.sh

COPY files/initonce/0010-generate-pw.sh /nitrous/initonce/0010-generate-pw.sh

COPY files/sources.list /etc/apt/sources.list

# Add fake Upstart job that emits events so that other services will run.
COPY files/fake-container-events.conf /etc/init/fake-container-events.conf


# Install essential tools
RUN \
  apt-get update && \
  apt-get -y dist-upgrade && \
  DEBIAN_FRONTEND=noninteractive apt-get install -yy --no-install-recommends \
    build-essential \
    autoconf \
    checkinstall \
    curl \
    wget \
    tmux \
    lsof \
    zsh \
    silversearcher-ag \
    zip\
    unzip \
    bzip2 \
    unison \
    man-db \
    vim-nox \
    emacs24-nox \
    nano \
    git \
    libssl-dev \
    rsync \
    dnsutils \
  && apt-get clean && apt-get autoremove

COPY files/gitconfig /home/$NITROUS_USERNAME/.gitconfig
COPY files/tmux.conf /home/$NITROUS_USERNAME/.tmux.conf
COPY files/vimrc /home/$NITROUS_USERNAME/.vimrc

RUN \
  /bin/bash -c 'chown -R $NITROUS_USERNAME:$NITROUS_USERNAME /home/$NITROUS_USERNAME/.gitconfig /home/$NITROUS_USERNAME/.tmux.conf /home/$NITROUS_USERNAME/.vimrc'

USER $NITROUS_USERNAME

# hushlogin
RUN \
  /bin/bash -c 'touch /home/$NITROUS_USERNAME/.hushlogin'

# Install oh-my-zsh
RUN \
  /bin/bash -c 'git clone https://github.com/robbyrussell/oh-my-zsh.git /home/$NITROUS_USERNAME/.oh-my-zsh && \
  cp /home/$NITROUS_USERNAME/.oh-my-zsh/templates/zshrc.zsh-template /home/$NITROUS_USERNAME/.zshrc && \
  sed -i "s|# DISABLE_AUTO_UPDATE|DISABLE_AUTO_UPDATE|g" /home/$NITROUS_USERNAME/.zshrc && \
  sudo chsh -s /bin/zsh $NITROUS_USERNAME && \
  sudo touch /etc/profile.d/dummy.sh && \
  sudo /bin/bash -c "echo source /etc/profile >> /etc/zsh/zprofile"'

# setup vim
RUN \
  /bin/bash -c 'git clone --branch v0.10.2 --depth 1 https://github.com/gmarik/Vundle.vim.git /home/$NITROUS_USERNAME/.vim/bundle/Vundle.vim && \
  vim -i NONE -c PluginInstall -c quitall > /dev/null'

# make code dir
RUN \
  mkdir /home/$NITROUS_USERNAME/code && \
  chown $NITROUS_USERNAME:$NITROUS_USERNAME /home/$NITROUS_USERNAME/code

USER root

# Install Nitrous Solo
COPY nitrous-solo /opt/nitrous-solo
RUN /opt/nitrous-solo/nitrousadmin adduser nitrous nitrous nitrous-password

CMD ["/sbin/init", "--default-console", "none"]
