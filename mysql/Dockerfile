FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y wget tar

# install MySQL
#RUN wget http://dev.mysql.com/get/Downloads/MySQL-5.6/MySQL-5.6.27-1.el6.x86_64.rpm-bundle.tar
#RUN tar xvf MySQL-5.6.27-1.el6.x86_64.rpm-bundle.tar
#RUN yum localinstall -y MySQL-shared-compat-5.6.27-1.el6.x86_64.rpm
#RUN yum localinstall -y MySQL-shared-5.6.27-1.el6.x86_64.rpm
#RUN yum localinstall -y MySQL-server-5.6.27-1.el6.x86_64.rpm
#RUN yum localinstall -y MySQL-client-5.6.27-1.el6.x86_64.rpm
#RUN yum localinstall -y MySQL-devel-5.6.27-1.el6.x86_64.rpm

RUN wget http://dev.mysql.com/get/Downloads/MySQL-5.5/MySQL-5.5.46-1.el6.x86_64.rpm-bundle.tar
RUN tar xvf MySQL-5.5.46-1.el6.x86_64.rpm-bundle.tar
RUN yum localinstall -y MySQL-shared-compat-5.5.46-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-shared-5.5.46-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-server-5.5.46-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-client-5.5.46-1.el6.x86_64.rpm
RUN yum localinstall -y MySQL-devel-5.5.46-1.el6.x86_64.rpm

# create mysql
ADD privilege.development.sql /tmp/
RUN /etc/init.d/mysql start \
   && mysql -u root < /tmp/privilege.development.sql

EXPOSE 3306
CMD ["/usr/bin/mysqld_safe"]
