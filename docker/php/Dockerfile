FROM php:7.3-fpm-buster

RUN apt-get update \
  && apt-get install -y zip unzip libzip-dev sqlite3 libsqlite3-dev libpq-dev libxslt-dev libmagickwand-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libc-client2007e-dev libkrb5-dev \
  && pecl install imagick xdebug-beta redis-5.1.1 \
  && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
  && docker-php-ext-enable imagick xdebug redis \
  && docker-php-ext-install gd mbstring pdo_mysql pdo_pgsql pdo_sqlite xml zip imap
