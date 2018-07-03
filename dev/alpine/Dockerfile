FROM       node:8-alpine
LABEL maintainer="wlwanaly@gmail.com"

RUN apk add --no-cache openssh-server supervisor python3 \
    python3-dev py-pip bash\
    && npm config set registry https://registry.npm.taobao.org  \
    && sed -i s/#PermitRootLogin.*/PermitRootLogin\ yes/ /etc/ssh/sshd_config \
    && echo 'root:root' |chpasswd \
    && ssh-keygen -A \ 
    && mkdir /var/run/sshd && mkdir -p /var/log/supervisor && \
    rm -rf /usr/bin/python && ln -s /usr/bin/python3  /usr/bin/python

COPY supervisord.conf /etc/supervisord.conf

EXPOSE 22

CMD    ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
