FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y vim git sudo passwd wget make gcc tar readline-devel
RUN yum install -y openssl-devel openssh openssh-server openssh-clients
RUN yum install -y ImageMagick ImageMagick-devel
RUN yum install -y install libxml2 libxml2-devel libxslt libxslt-devel

# install MySQL
RUN wget http://dev.mysql.com/get/Downloads/MySQL-5.5/MySQL-5.5.39-2.el6.x86_64.rpm-bundle.tar
RUN tar xvf MySQL-5.5.39-2.el6.x86_64.rpm-bundle.tar
RUN yum localinstall -y MySQL-shared-compat-5.5.39-2.el6.x86_64.rpm
RUN yum localinstall -y MySQL-shared-5.5.39-2.el6.x86_64.rpm
RUN yum localinstall -y MySQL-server-5.5.39-2.el6.x86_64.rpm
RUN yum localinstall -y MySQL-client-5.5.39-2.el6.x86_64.rpm
RUN yum localinstall -y MySQL-devel-5.5.39-2.el6.x86_64.rpm

# create user
RUN useradd -m -s /bin/bash oomatomo
RUN echo 'oomatomo' | passwd --stdin oomatomo

# setup sudo config
RUN echo "oomatomo ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# setup rbenv
## rben install
RUN su oomatomo -c "git clone https://github.com/sstephenson/rbenv.git ~/.rbenv"
RUN su oomatomo -c "git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build"

RUN echo 'export PATH="~/.rbenv/bin:$PATH"' >> /home/oomatomo/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> /home/oomatomo/.bashrc
RUN echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> /home/oomatomo/.bashrc

RUN chown oomatomo:oomatomo /home/oomatomo/.bashrc
## ruby install
RUN su oomatomo -c "/home/oomatomo/.rbenv/bin/rbenv install 2.1.1"
RUN su oomatomo -c "/home/oomatomo/.rbenv/bin/rbenv global 2.1.1"
RUN su oomatomo -c "/home/oomatomo/.rbenv/shims/gem install bundle"

# setup nodebrew
RUN su oomatomo -c "curl -L https://raw.githubusercontent.com/hokaccha/nodebrew/master/nodebrew | perl - setup"
## node install
RUN su oomatomo -c "/home/oomatomo/.nodebrew/current/bin/nodebrew install-binary stable"
RUN su oomatomo -c "/home/oomatomo/.nodebrew/current/bin/nodebrew use stable"
RUN su oomatomo -c "/home/oomatomo/.nodebrew/current/bin/npm install -g coffee-script"

# setup SSH
RUN sed -ri 's/PasswordAuthentication yes/PasswordAuthentication yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
RUN sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config

# Init SSHD
RUN /etc/init.d/sshd start
RUN /etc/init.d/sshd stop

# start MySQL
RUN /etc/init.d/mysql start

EXPOSE 22 3000

CMD ["/usr/sbin/sshd","-D"]
