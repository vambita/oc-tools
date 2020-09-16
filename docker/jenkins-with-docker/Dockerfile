FROM jenkins/jenkins:latest
LABEL maintainer="solutions@vambita.com"

ARG JENKINS_VERSION=2.255

USER root
RUN apt-get update && apt-get upgrade -y && apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common \
    && curl -sL https://deb.nodesource.com/setup_12.x | bash - && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 73C3DB2A && add-apt-repository ppa:linuxuprising/java && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian  $(lsb_release -cs) stable" && apt-get update && apt-get upgrade -y \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && echo oracle-java14-installer shared/accepted-oracle-license-v1-2 select true | /usr/bin/debconf-set-selections \
    && echo oracle-java14-installer shared/accepted-oracle-licence-v1-2 boolean true | /usr/bin/debconf-set-selections \
    && apt-get update && apt-get upgrade -y && apt-get install -y oracle-java14-installer oracle-java14-set-default docker-ce docker-ce-cli containerd.io nodejs \
    && usermod -aG docker jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins/customs-plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins/customs-plugins.txt