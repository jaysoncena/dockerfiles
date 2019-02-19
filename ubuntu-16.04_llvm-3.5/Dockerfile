FROM ubuntu:xenial
MAINTAINER Jayson Cena <jayson@cena.ph>

ENV TZ=UTC
ENV DEBIAN_FRONTEND=noninteractive
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
	&& echo $TZ > /etc/timezone


RUN apt-get update
RUN apt-get -y install \
	llvm-3.5-dev \
	clang-3.5 \
	libncurses5 \
	libncurses5-dev \
	graphviz \
	vim \
	less

CMD ["/bin/bash"]
