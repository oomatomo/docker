FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y vim openssh openssh-server openssh-clients sudo passwd wget tar openssl-devel readline-devel

RUN wget http://dev.mysql.com/get/Downloads/MySQL-5.6/MySQL-5.6.21-1.el6.x86_64.rpm-bundle.tar
RUN tar xvf MySQL-5.6.21-1.el6.x86_64.rpm-bundle.tar
RUN yum localinstall -y MySQL-shared-compat-5.6.21-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-shared-5.6.21-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-server-5.6.21-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-client-5.6.21-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-devel-5.6.21-1.el6.x86_64.rpm

# create user
RUN useradd -m -s /bin/bash oomatomo
RUN echo 'oomatomo' | passwd --stdin oomatomo

RUN mkdir -p /home/oomatomo/.ssh
RUN chown oomatomo:oomatomo -R /home/oomatomo/.ssh; chmod 700 /home/oomatomo/.ssh

# setup sudo config
RUN echo "oomatomo ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# setup SSH
RUN sed -ri 's/PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

# Init SSHD
RUN /etc/init.d/sshd start
RUN /etc/init.d/sshd stop

EXPOSE 22 3000

CMD ["/usr/sbin/sshd","-D"]
