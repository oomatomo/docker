FROM centos:centos6
MAINTAINER oomatomo ooma0301@gmail.com

RUN rpm -Uhv http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN yum update -y
# java
RUN yum install -y wget tar java-1.8.0-openjdk java-1.8.0-openjdk-devel

RUN wget http://dynamodb-local.s3-website-us-west-2.amazonaws.com/dynamodb_local_latest.tar.gz

ENV DYNAMODB_PATH /usr/local/dynamodb
RUN mkdir -p $DYNAMODB_PATH
RUN tar zxf dynamodb_local_latest.tar.gz -C $DYNAMODB_PATH
WORKDIR /usr/local/dynamodb

EXPOSE 8000
CMD ["java", "-Djava.library.path=.", "-jar", "DynamoDBLocal.jar", "-sharedDb"]
