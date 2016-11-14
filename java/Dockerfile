FROM nitrous/nodejs:latest
MAINTAINER Nitrous, Inc. <eng@nitrous.io>

# https://github.com/docker/docker/issues/1024
# see https://bugs.launchpad.net/ubuntu/+source/upstart/+bug/430224/comments/6
# and https://bugs.launchpad.net/ubuntu/+source/systemd/+bug/1325142/comments/38
RUN \
  cp /sbin/initctl /sbin/initctlbak && \
  dpkg-divert --local --rename --add /sbin/initctl && \
  ln -sf /bin/true /sbin/initctl && \
  dpkg-divert --local --add /etc/init.d/systemd-logind && \
  ln -s /bin/true /etc/init.d/systemd-logind

RUN \
  apt-get update && \
  apt-get install -y --no-install-recommends openjdk-7-jdk && \
  apt-get clean

RUN mv /sbin/initctlbak /sbin/initctl


ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

RUN echo 'export PATH=$JAVA_HOME/bin:$PATH' >> /etc/profile
