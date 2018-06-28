FROM       node:8-alpine
LABEL maintainer="wlwanaly@gmail.com"

RUN apk add --no-cache openssh-server supervisor python3 \
    python3-dev py-pip\
    && npm config set registry https://registry.npm.taobao.org 
    
RUN mkdir /var/run/sshd && mkdir -p /var/log/supervisor && \
    rm -rf /usr/bin/python && ln -s /usr/bin/python3  /usr/bin/python

RUN ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key && \
    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key

COPY supervisord.conf /etc/supervisord.conf

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
