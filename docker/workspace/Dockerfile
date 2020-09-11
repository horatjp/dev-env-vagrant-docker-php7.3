FROM debian:buster

ENV PKG="vim git gpg curl zip unzip imagemagick locales"
ENV PHP_PKG="php-cli php-curl php-mbstring php-zip php-xml php-gd php-imagick php-pgsql php-mysql php-sqlite3 php-memcached php-xdebug php-redis php-imap"

RUN apt update \
    && apt -y install $PKG $PHP_PKG

RUN echo "ja_JP.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


# composer
ENV COMPOSER_ALLOW_SUPERUSER 1
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

# nodejs install
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get install -y nodejs


ENV LANG=ja_JP.UTF-8
