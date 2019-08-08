# Version:0.0.1
FROM centos:6.8
MAINTAINER Wang Xmeming "wangxuemingcn@yeah.net"
ENV REFRESHED_AT 2019-08-08
RUN echo root | passwd root --stdin
ADD jdk-8u181-linux-x64.tar.gz /root
# RUN tar -xzvf /root/jdk-8u181-linux-x64.tar.gz /root
#RUN rm -f jdk-8u181-linux-x64.tar.gz
RUN echo -e '\nJAVA_HOME=/root/jdk1.8.0_181\nexport JAVA_HOME\nPATH=$JAVA_HOME/bin:$PATH\nexport PATH' >> /etc/bashrc
RUN yum -y install openssh-server
RUN service sshd start
CMD ["/usr/sbin/sshd", "-D"]
EXPOSE 22
