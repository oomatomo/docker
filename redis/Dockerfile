FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

# install package
RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
RUN yum install -y wget tar make gcc

RUN cd /tmp && \
      wget http://download.redis.io/redis-stable.tar.gz && \
      tar xvzf redis-stable.tar.gz && \
      cd redis-stable && \
      make && \
      make install && \
      cp -f src/redis-sentinel /usr/local/bin && \
      mkdir -p /etc/redis && \
      cp -f *.conf /etc/redis

# change bind
RUN sed s/bind\ 127.0.0.1/bind\ 0.0.0.0/ -i /etc/redis/redis.conf

EXPOSE 6379
CMD ["redis-server", "/etc/redis/redis.conf"]
