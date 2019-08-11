FROM ubuntu:14.04
MAINTAINER james@example.com

ENV REFRESHED_AT 2019-08-11
RUN apt-get update -qq && apt-get install -qqy apt-transport-https curl software-properties-common
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

RUN apt-get update -qq && apt-get install -qqy iptables ca-certificates lxc git-core
ADD jdk-8u181-linux-x64.tar.gz /root
# RUN tar -xzvf /root/jdk-8u181-linux-x64.tar.gz /root
#RUN rm -f jdk-8u181-linux-x64.tar.gz
#RUN echo '\nJAVA_HOME=/root/jdk1.8.0_181\nexport JAVA_HOME\nPATH=$JAVA_HOME/bin:$PATH\nexport PATH' >> /etc/bash.bashrc
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
RUN apt-get update -qq
RUN apt-get install -y docker-ce=18.03.1~ce-0~ubuntu

ENV JENKINS_HOME /opt/jenkins/data
ENV JENKINS_MIRROR http://mirrors.jenkins-ci.org

RUN mkdir -p $JENKINS_HOME/plugins
RUN curl -sf -o /opt/jenkins/jenkins.war -L $JENKINS_MIRROR/war-stable/latest/jenkins.war

RUN for plugin in chucknorris greenballs scm-api git-client git ws-cleanup ;\
    do curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi \
       -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi ; done

ADD ./dockerjenkins.sh /usr/local/bin/dockerjenkins.sh
RUN chmod +x /usr/local/bin/dockerjenkins.sh

EXPOSE 8080
VOLUME /var/lib/docker

CMD [ "/usr/local/bin/dockerjenkins.sh" ]
