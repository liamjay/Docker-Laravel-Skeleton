FROM php:7-apache

RUN apt-get update \
 && apt-get install -y --no-install-recommends libmemcached-dev zlib1g-dev \
    libicu-dev libmcrypt-dev libxml2-dev curl libcurl4-openssl-dev \
 && rm -r /var/lib/apt/lists/* \
 && docker-php-ext-configure intl \
 && docker-php-ext-install zip pdo pdo_mysql mysqli mbstring mcrypt intl soap xml curl \
 && pecl install memcached xdebug \
 && docker-php-ext-enable memcached xdebug \
 && echo "xdebug.remote_enable=1"  >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
 && echo "xdebug.remote_host=127.0.0.1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

COPY app/ /var/www/html
WORKDIR /var/www/html

RUN sed -i -e "s/html/html\/public/g" /etc/apache2/sites-enabled/000-default.conf
RUN a2enmod rewrite

RUN chmod -R 777 storage

EXPOSE 80