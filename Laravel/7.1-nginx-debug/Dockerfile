# usage
# docker run -d -v /you/laravel/folder:/var/www/laravel -p 80:80 -p 443:443 toninho09/apache-laravel
FROM ubuntu:18.04
MAINTAINER Antonio <antoniohls@gmail.com>

COPY endpoint.sh /endpoint.sh

RUN apt-get update \
&& apt-get -y install git curl nginx php-fpm php-mysql php-curl php-gd php-intl php-pear php-imagick php-imap php-mcrypt php-memcache php-pgsql \
php-pspell php-recode php-sqlite3 php-tidy php-xmlrpc php-xsl php-mbstring php-gettext php-odbc php-sybase php-xml php-json php-zip php-xdebug tdsodbc \
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

COPY 20-xdebug.ini /etc/php/7.1/cli/conf.d/20-xdebug.ini

WORKDIR /

EXPOSE 80
EXPOSE 443

CMD ["./endpoint.sh"]