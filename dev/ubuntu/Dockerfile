FROM       node:8
LABEL maintainer="wlwanaly@gmail.com"

RUN apt-get update && apt-get install -y --no-install-recommends  \
    openssh-server supervisor \ 
    && rm -rf /var/lib/apt/lists/* \
    && npm config set registry https://registry.npm.taobao.org 
    
RUN mkdir /var/run/sshd
RUN mkdir -p /var/log/supervisor

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22

CMD    ["/usr/bin/supervisord"]
