FROM php:7.2-fpm

MAINTAINER "William Silva" <williamsilva808@hotmail.com>

# Install PHP extensions
RUN apt-get update && apt-get install -y \
        vim \
        git \
    --no-install-recommends

RUN docker-php-ext-install pdo_mysql

RUN docker-php-ext-install mysqli

RUN apt-get install -y \
        libintl-perl \
        libicu-dev \
    && docker-php-ext-configure intl \
    && docker-php-ext-install intl

RUN apt-get install -y \
        libzip-dev \
        unzip \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip

RUN apt-get install -y \
        libmagickwand-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick

RUN apt-get install -y \
        libmcrypt-dev \
    && pecl install mcrypt-1.0.0 \
    && docker-php-ext-enable mcrypt

RUN docker-php-ext-install opcache

RUN pecl install apcu \
    && docker-php-ext-enable apcu

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# install phpunit
RUN curl https://phar.phpunit.de/phpunit.phar -L > phpunit.phar \
  && chmod +x phpunit.phar \
  && mv phpunit.phar /usr/local/bin/phpunit \
  && phpunit --version

# Change uid and gid of apache to docker user uid/gid
RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

WORKDIR /var/www/html
