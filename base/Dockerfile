FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y

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

EXPOSE 22

CMD ["/usr/sbin/sshd","-D"]
