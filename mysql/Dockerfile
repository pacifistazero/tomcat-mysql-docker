FROM alpine:latest
MAINTAINER iandrian

RUN apk update && \
	apk add mysql mysql-client && \
	addgroup mysql mysql && \
	rm -rf /var/cache/apk/*

VOLUME ["/var/lib/mysql"]

EXPOSE 3306

RUN /setup-mysql.sh