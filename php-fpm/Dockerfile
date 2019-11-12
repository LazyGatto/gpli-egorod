FROM php:7.3.2-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libldap2-dev \
        libc-client-dev \
        libkrb5-dev \
        libsnmp-dev \
        libxml2-dev \
    ; \
    rm -r /var/lib/apt/lists/* ; \
    docker-php-ext-install -j$(nproc) iconv ; \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ ; \
    docker-php-ext-configure ldap ; \
    docker-php-ext-install -j$(nproc) \
       exif \
       gd \
       imap \
       ldap \
       mysqli \
       opcache \
       snmp \
       soap \
       xmlrpc \
    ; \
    pecl install apcu-4.0.11 && docker-php-ext-enable apcu ; \

### TEMP STRING MOVED TO ASSETS
# RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini" 

COPY assets/php.ini /usr/local/etc/php/php.ini
COPY assets/index.php /var/www/html/index.php

# Override with custom opcache settings
# COPY assets/opcache.ini $PHP_INI_DIR/conf.d/