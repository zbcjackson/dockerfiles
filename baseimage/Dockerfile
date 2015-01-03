FROM phusion/baseimage
MAINTAINER Jackson Zhang <zbcjackson@gmail.com>

RUN sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y vim git-core curl procps gcc openjdk-6-jdk\
  build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev autoconf imagemagick libbz2-dev \
  libcurl4-openssl-dev libevent-dev libffi-dev libglib2.0-dev libjpeg-dev libmagickcore-dev libmagickwand-dev \
  libmysqlclient-dev libncurses-dev libpq-dev libsqlite3-dev libxml2-dev libxslt-dev \ 
 && rm -rf /var/lib/apt/lists/*
RUN update-alternatives --set editor /usr/bin/vim.basic
