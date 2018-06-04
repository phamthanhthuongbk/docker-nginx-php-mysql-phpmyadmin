FROM php:7.0-fpm
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng-dev \
        vim \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

# composer 1.6.4
RUN curl -sS https://raw.githubusercontent.com/composer/getcomposer.org/58c3cc59978616c132b5fed9b09314e24cb60462/web/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN pecl install -o -f redis-4.0.2 \
	&& rm -rf /tmp/pear

RUN pecl install -o -f xdebug-2.6.0 \
  && rm -rf /tmp/pear

RUN mkdir -p /var/log/php \
  && chown www-data:root /var/log/php \
  && chmod 755 /var/log/php

RUN ln -sf /dev/stderr /var/log/php/error.log \
  && ln -sf /dev/stderr /var/log/php/www-error.log \
  && ln -sf /dev/stderr /var/log/php/php_errors.log
