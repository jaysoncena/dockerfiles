FROM ubuntu-debootstrap:14.04.3
MAINTAINER Jayson Cena

ENV DEBIAN_FRONTEND noninteractive

RUN echo "Etc/UTC" > /etc/timezone
RUN dpkg-reconfigure tzdata

## Keep upstart from complaining
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN rm /sbin/initctl
RUN ln -s /bin/true /sbin/initctl

## Add SaltStack Repo
ADD https://repo.saltstack.com/apt/ubuntu/14.04/amd64/latest/SALTSTACK-GPG-KEY.pub /SALTSTACK-GPG-KEY.pub
RUN apt-key add SALTSTACK-GPG-KEY.pub
RUN echo "deb http://repo.saltstack.com/apt/ubuntu/14.04/amd64/latest trusty main" > /etc/apt/sources.list.d/saltstack.list
RUN apt-get update && apt-get install -y salt-master salt-minion salt-ssh salt-cloud gpgv

## Verify and install Tini init
ENV TINI_VERSION v0.9.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini.asc /tini.asc
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 0527A9B7 \
 && gpg --verify /tini.asc

RUN chmod +x /tini
ENTRYPOINT ["/tini", "-v", "--"]

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 4505 4506

CMD ["/usr/bin/salt-master"]
