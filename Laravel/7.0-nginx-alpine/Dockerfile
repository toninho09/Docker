# usage
# docker run -d -v /you/laravel/folder:/var/www/laravel -p 80:80 -p 443:443 toninho09/apache-laravel
#
#
#apk update
#apk add nginx
#apk add php7-fpm php7-pdo_mysql php7-curl php7-gd php7-intl php7-pear php7-imagick php7-imap php7-mcrypt php7-memcached php7-pspell php7-recode php7-sqlite3 php7-tidy php7-xmlrpc php7-xsl php7-mbstring php7-gettext php7-odbc php7-xml php7-json
#mkdir /run/nginx
#mkdir /run/php
#/etc/php7/php-fpm.d/www.conf   <  listen = /run/php/php7.0-fpm.sock
#
#
FROM ubuntu:17.04
MAINTAINER Antonio <antoniohls@gmail.com>

COPY endpoint.sh /endpoint.sh

RUN apt-get update \
&& apt-get -y install git curl nginx php7-fpm php7-pdo_mysql php7-curl php7-gd php7-intl php7-pear php7-pgsql php7-imagick php7-imap php7-mcrypt php7-memcached php7-pspell php7-recode php7-sqlite3 php7-tidy php7-xmlrpc php7-xsl php7-mbstring php7-gettext php7-odbc php7-xml php7-json tdsodbc \
&& apt-get -y autoremove \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& mkdir -p /run/php \
&& /usr/bin/curl -sS https://getcomposer.org/installer | /usr/bin/php \
&& /bin/mv composer.phar /usr/local/bin/composer \
&& chmod +x \endpoint.sh \
&& rm /etc/nginx/sites-available/default


ADD 000-laravel.conf /etc/nginx/sites-available/
#ADD 001-laravel-ssl.conf /etc/nginx/sites-available/
COPY freetds.conf /etc/freetds/freetds.conf

RUN ln -s /etc/nginx/sites-available/000-laravel.conf /etc/nginx/sites-enabled/000-laravel.conf

WORKDIR /

EXPOSE 80
EXPOSE 443

CMD ["./endpoint.sh"]