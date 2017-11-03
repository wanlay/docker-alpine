FROM jenkins
MAINTAINER wanlay <wlwanlay@gmail.com>
# if we want to install via apt
USER root
RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
  && echo 'Asia/Shanghai' >/etc/timezone 
RUN apt-get update && apt-get install -y zip \
  && echo "docker:x:${dockerGid}:jenkins" >> /etc/group 
# drop back to the regular jenkins user - good practice
USER jenkins
