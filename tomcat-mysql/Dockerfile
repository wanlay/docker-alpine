FROM tomcat:8-alpine
WORKDIR /app
VOLUME /app
VOLUME /usr/local/tomcat/logs
VOLUME /usr/local/tomcat/webapps
COPY mysql-start.sh /mysql-start.sh

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories && \
    apk add --update mysql mysql-client supervisor && rm -f /var/cache/apk/*
COPY my.cnf /etc/mysql/my.cnf

ADD supervisord.ini /etc/supervisor.d/supervisord.ini


EXPOSE 3306 8080
CMD ["supervisord","-n"]