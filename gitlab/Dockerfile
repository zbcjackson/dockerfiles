FROM phusion/baseimage
MAINTAINER Jackson Zhang <zbcjackson@gmail.com>

RUN sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y vim git-core curl procps gcc \
  build-essential zlib1g-dev libssl-dev libreadline-dev libyaml-dev autoconf imagemagick libbz2-dev \
  libcurl4-openssl-dev libevent-dev libffi-dev libglib2.0-dev libjpeg-dev libmagickcore-dev libmagickwand-dev \
  libmysqlclient-dev libncurses-dev libpq-dev libsqlite3-dev libxml2-dev libxslt-dev \ 
 && rm -rf /var/lib/apt/lists/*
RUN update-alternatives --set editor /usr/bin/vim.basic



RUN apt-get update && apt-get install -y supervisor logrotate locales nginx openssh-server mysql-client postgresql-client redis-tools \
 && update-locale LANG=C.UTF-8 LC_MESSAGES=POSIX \
 && locale-gen en_US.UTF-8 \
 && dpkg-reconfigure locales \
 && rm -rf /var/lib/apt/lists/*



ENV RUBY_MAJOR 2.1
ENV RUBY_VERSION 2.1.5

# some of ruby's build scripts are written in ruby
# we purge this later to make sure our final image uses what we just built
RUN apt-get update \
  && apt-get install -y bison ruby \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p /usr/src/ruby \
  && curl -SL "http://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.bz2" \
          | tar -xjC /usr/src/ruby --strip-components=1 \
  && cd /usr/src/ruby \
  && autoconf \
  && ./configure --disable-install-doc \
  && make -j"$(nproc)" \
  && apt-get purge -y --auto-remove bison ruby \
  && make install \
  && rm -r /usr/src/ruby

# skip installing gem documentation
RUN echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc"

# install things globally, for great justice
ENV GEM_HOME /usr/local/bundle
ENV PATH $GEM_HOME/bin:$PATH
RUN gem install bundler \
  && bundle config --global path "$GEM_HOME" \
  && bundle config --global bin "$GEM_HOME/bin"

# don't create ".bundle" in all our apps
ENV BUNDLE_APP_CONFIG $GEM_HOME



RUN adduser --disabled-login --gecos 'GitLab' gitlab





CMD ["/bin/bash"]
