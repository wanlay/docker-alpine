FROM       ubuntu:16.04
LABEL maintainer="wlwanaly@gmail.com"

# 将源修改为中科大
RUN sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list \
    && sed -i 's/security.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends software-properties-common \
    openssh-server supervisor curl
    
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -  \
    apt-get install -y nodejs \
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
