
FROM   centos:7
MAINTAINER Mark McCahill "mark.mccahill@duke.edu"

USER root

RUN yum -y update && \
    yum -y install wget \
    yum clean all

#
# JDK
#
RUN wget --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
         http://download.oracle.com/otn-pub/java/jdk/8u73-b02/jdk-8u73-linux-x64.rpm

RUN  rpm -ivh jdk-8*  ; \
     rm jdk-8*

#
# Jetty
#
RUN wget http://download.eclipse.org/jetty/stable-9/dist/jetty-distribution-9.3.7.v20160115.tar.gz 


#
# things we need assuming we end up running systemd
#
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
#CMD ["/usr/sbin/init"]

# 
# testing only
#
#RUN yum -y install httpd; \ 
#    yum clean all; \
#    systemctl enable httpd.service
#EXPOSE 80
CMD ["/usr/sbin/init"]

