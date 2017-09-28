FROM jenkins/jenkins:lts
MAINTAINER Iain Coffield

USER root

### Install Plugins ###
# Install dos2unix to fix line endings
RUN apt-get update && apt-get install -y \
  dos2unix \
  && rm -rf /var/lib/apt/lists/*
# Copy over the plugins to install for Jenkins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
# Fix any Line endings that we have
RUN dos2unix /usr/share/jenkins/ref/plugins.txt
# Install the plugins
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
### /Install Plugins ###

### Jenkins log files ###
# make a directory to house the logs so that we don't lose them when running in detach mode
RUN mkdir /var/log/jenkins
# jenkins user should own the directory
RUN chown -R  jenkins:jenkins /var/log/jenkins
### /Jenkins log files ###

USER jenkins

### Jenkins Environmental variables ###
ENV JENKINS_OPTS="--logfile=/var/log/jenkins/jenkins.log"
### /Jenkins Environmental variables ###