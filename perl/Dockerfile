FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y tar bzip2 gcc make perl perl-ExtUtils-MakeMaker

RUN curl -L http://cpanmin.us | perl - App::cpanminus
RUN cpanm Carton
