FROM php:8.2.1-fpm

WORKDIR /var/www/html

RUN apt-get update && apt-get install -y \
      apt-utils \
      libpq-dev \
      libpng-dev \
      libzip-dev \
      zip unzip \
      npm \
      git && \
      docker-php-ext-install pdo_mysql && \
      docker-php-ext-install bcmath && \
      docker-php-ext-install gd && \
      docker-php-ext-install zip && \
      apt-get clean && \
      rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN pecl install xdebug-3.2.0 && docker-php-ext-enable xdebug

COPY ./docker/php/conf.d/* $PHP_INI_DIR/conf.d/
COPY ./docker/php/php.ini /usr/local/etc/php/conf.d/php.ini

CMD ["php-fpm"]


ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin
