FROM php:7-fpm

COPY ./php/php.ini /usr/local/etc/php/php.ini

RUN apt-get update -y \
    && apt-get install -y \
        libzip-dev \
        libpng-dev \
        libmagickwand-dev \
        libicu-dev \
        libmemcached-dev \
        libjpeg62-turbo-dev \
        libfreetype6-dev

RUN docker-php-ext-configure gd --with-freetype=/usr --with-jpeg=/usr \
    && docker-php-ext-configure intl

RUN docker-php-ext-install mysqli pdo pdo_mysql \
    && docker-php-ext-install bcmath \
    && docker-php-ext-install gd \
    && docker-php-ext-install zip \
    && docker-php-ext-install intl

RUN pecl install imagick \
    && docker-php-ext-enable imagick

RUN pecl install memcached \
    && docker-php-ext-enable memcached

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && echo "xdebug.mode = debug" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.client_host = host.docker.internal" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini