FROM centos:centos7
MAINTAINER The CentOS Project <cloud-ops@centos.org>

ENV TZ Asia/Tokyo
RUN yum -y update; yum clean all
RUN yum -y install openssh-server openssh-client passwd; yum clean all

RUN yum update -y && yum -y install epel-release which man-pages && \
    yum -y --setopt=tsflags='' groups install "Development Tools" && \
    yum -y --setopt=tsflags='' install vim wget sudo rpmdevtools ansible && \
    yum clean all

ADD ./start.sh /start.sh
RUN mkdir /var/run/sshd

RUN ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key -N '' 

RUN chmod 755 /start.sh
# EXPOSE 22
RUN ./start.sh
RUN echo "user ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers

ENTRYPOINT ["/usr/sbin/sshd", "-D"]
