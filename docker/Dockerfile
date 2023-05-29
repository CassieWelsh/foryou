FROM php:8-apache

RUN apt-get update && apt-get install -y \
    	nano
RUN a2enmod rewrite
RUN apt-get install -y libpq-dev \
    && docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
    && docker-php-ext-install pdo pdo_pgsql pgsql

RUN apt-get install 

RUN a2enmod ssl

USER root

RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

WORKDIR /var/www/html/public

COPY default.conf /etc/apache2/sites-enabled/000-default.conf
COPY my.key /etc/ssl/certs/my.key
COPY certificate.crt /etc/ssl/certs/certificate.crt

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

EXPOSE 80
