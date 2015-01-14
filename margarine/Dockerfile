FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y vim git sudo passwd wget make gcc tar readline-devel
RUN yum install -y openssl-devel openssh openssh-server openssh-clients
RUN yum install -y mysql mysql-server mysql-devel
RUN yum install -y ImageMagick ImageMagick-devel
RUN yum install -y install libxml2 libxml2-devel libxslt libxslt-devel

# create user
RUN useradd -m -s /bin/bash margarine
RUN echo 'margarine' | passwd --stdin margarine

# setup sudo config
RUN echo "margarine ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
# setup SSH

# setup rbenv and nodebrew
RUN su margarine -c "git clone https://github.com/sstephenson/rbenv.git ~/.rbenv"
RUN su margarine -c "git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build"
RUN su margarine -c "curl -L https://raw.githubusercontent.com/hokaccha/nodebrew/master/nodebrew | perl - setup"
RUN echo 'export PATH="~/.rbenv/bin:$PATH"' >> /home/margarine/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> /home/margarine/.bashrc
RUN echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> /home/margarine/.bashrc
RUN chown margarine:margarine /home/margarine/.bashrc
# ruby install
RUN su margarine -c "/home/margarine/.rbenv/bin/rbenv install 2.1.1"
RUN su margarine -c "/home/margarine/.rbenv/bin/rbenv global 2.1.1"
RUN su margarine -c "/home/margarine/.rbenv/shims/gem install bundle"
RUN su margarine -c "/home/margarine/.nodebrew/current/bin/nodebrew install-binary stable"
RUN su margarine -c "/home/margarine/.nodebrew/current/bin/nodebrew use stable"
RUN su margarine -c "/home/margarine/.nodebrew/current/bin/npm install -g coffee-script"

# Init SSHD
RUN /etc/init.d/sshd start
RUN /etc/init.d/sshd stop

EXPOSE 22 3000

CMD ["/usr/sbin/sshd","-D"]
