# usage
# docker run -d -v /you/laravel/folder:/var/www/laravel -p 80:80 -p 443:443 toninho09/apache-laravel
FROM ubuntu:16.04
MAINTAINER Antonio <antoniohls@gmail.com>

RUN apt-get update \
&& apt-get -y install zip git curl apache2 php php-soap php-mysql php-mcrypt php-json php-curl php-gd php-odbc php-pgsql php-sybase tdsodbc php-xml php-sqlite3 php-zip php-xdebug libapache2-mod-php php-mbstring\
&& apt-get -y autoremove \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* \
&& /usr/sbin/a2enmod rewrite \
&& /usr/sbin/a2enmod mime \
&& /usr/sbin/a2dissite '*'

ADD 000-laravel.conf /etc/apache2/sites-available/
ADD 001-laravel-ssl.conf /etc/apache2/sites-available/
COPY freetds.conf /etc/freetds/freetds.conf

RUN /usr/sbin/a2ensite 000-laravel 001-laravel-ssl \
&& /usr/bin/curl -sS https://getcomposer.org/installer |/usr/bin/php \
&& /bin/mv composer.phar /usr/local/bin/composer

COPY 20-xdebug.ini /etc/php/7.0/cli/conf.d/20-xdebug.ini

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

EXPOSE 80
EXPOSE 443

WORKDIR /var/www/laravel

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
