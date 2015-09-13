FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
# java
RUN yum install -y wget tar java-1.8.0-openjdk java-1.8.0-openjdk-devel

ENV SCALA_VERSION 2.11.6
ENV SBT_VERSION 0.13.8

# scala
RUN wget http://www.scala-lang.org/files/archive/scala-$SCALA_VERSION.tgz
RUN tar xvf scala-$SCALA_VERSION.tgz
RUN mv scala-$SCALA_VERSION /usr/lib
RUN ln -s /usr/lib/scala-$SCALA_VERSION /usr/lib/scala
ENV PATH $PATH:/usr/lib/scala/bin

# sbt
RUN curl -O -L http://dl.bintray.com/sbt/rpm/sbt-$SBT_VERSION.rpm
RUN rpm -ivh sbt-$SBT_VERSION.rpm --nodeps
