FROM openjdk:8-jdk-alpine

MAINTAINER iandrian

ENV TOMCAT_VERSION_MAJOR=8
ENV TOMCAT_VERSION_FULL=8.0.45
ENV MYSQL_JDBC_DRIVER_VERSION=5.1.42

RUN mkdir -p /opt
WORKDIR /opt

# Download and Install Tomcat
RUN apk add --update curl && \
  curl -LO http://mirrors.standaloneinstaller.com/apache/tomcat/tomcat-${TOMCAT_VERSION_MAJOR}/v${TOMCAT_VERSION_FULL}/bin/apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz && \
  curl -LO https://www.apache.org/dist/tomcat/tomcat-${TOMCAT_VERSION_MAJOR}/v${TOMCAT_VERSION_FULL}/bin/apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz.md5 && \
  md5sum -c apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz.md5 && \
  gunzip -c apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz | tar -xf - -C /opt && \
  rm -f apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz apache-tomcat-${TOMCAT_VERSION_FULL}.tar.gz.md5 && \
  ln -s /opt/apache-tomcat-${TOMCAT_VERSION_FULL} /opt/tomcat && \
  rm -rf /opt/tomcat/webapps/examples /opt/tomcat/webapps/docs && \
  apk del curl && \
  rm -rf /var/cache/apk/*

## Tomcat Configuration
ADD tomcat-users.xml /opt/tomcat/conf/
RUN sed -i 's/52428800/5242880000/g' /opt/tomcat/webapps/manager/WEB-INF/web.xml

## Set environment
ENV CATALINA_HOME /opt/tomcat

## Expose Tomcat Public Port
EXPOSE 8080

## Copy MYSQL JDBC Driver
RUN apk add --update curl && \
  curl -LO https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-${MYSQL_JDBC_DRIVER_VERSION}.tar.gz && \
  gunzip -c mysql-connector-java-${MYSQL_JDBC_DRIVER_VERSION}.tar.gz | tar -xf - -C /opt && \  
  cd /opt && \
  cp mysql-connector-java-${MYSQL_JDBC_DRIVER_VERSION}/mysql-connector-java-${MYSQL_JDBC_DRIVER_VERSION}-bin.jar /opt/tomcat/lib && \
  rm -rf mysql-connector-java-${MYSQL_JDBC_DRIVER_VERSION}*

# Run Service
CMD ${CATALINA_HOME}/bin/catalina.sh run
