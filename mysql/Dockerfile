FROM zbcjackson/baseimage
MAINTAINER Jackson Zhang <zbcajckson@gmail.com>

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r mysql && useradd -r -g mysql mysql

ENV MYSQL_MAJOR 5.6

RUN apt-get update && apt-get install -y mysql-server-${MYSQL_MAJOR} pwgen && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql

ADD my.cnf /etc/mysql/conf.d/my.cnf
ADD mysqld_charset.cnf /etc/mysql/conf.d/mysqld_charset.cnf


VOLUME /var/lib/mysql

COPY entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld"]
