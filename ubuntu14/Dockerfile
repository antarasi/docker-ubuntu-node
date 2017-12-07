FROM ubuntu:14.04
MAINTAINER ANTARA IT Systems "contact@antara.pl"

ENV HOME /root

RUN apt-get update \
    && apt-get -qq update \
    && apt-get -y install sudo git curl openssh-server \
    && mkdir /var/run/sshd \
    && echo 'root:root' | chpasswd \
    && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash - \
    && apt-get update && apt-get install -y nodejs \
    && npm install npm@5.2.0 -g

RUN apt-get install -y ufw

RUN node -v && npm -v

CMD ["/bin/bash"]
WORKDIR /project
VOLUME ["/project"]

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]