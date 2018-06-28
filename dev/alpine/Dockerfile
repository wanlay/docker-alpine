FROM       node:8-alpine
LABEL maintainer="wlwanaly@gmail.com"

RUN apk add --no-cache openssh-server supervisor python3 \
    python3-dev \
    && npm config set registry https://registry.npm.taobao.org 
    
RUN mkdir /var/run/sshd
RUN mkdir -p /var/log/supervisor

COPY supervisord.conf /etc/supervisor.d/supervisord.conf

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/bin/supervisord", "-c", "/etc/supervisor.d/supervisord.conf"]
