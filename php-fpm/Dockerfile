FROM php:7.3.2-fpm

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd \
	&& mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"


# Override with custom opcache settings
# COPY assets/opcache.ini $PHP_INI_DIR/conf.d/

