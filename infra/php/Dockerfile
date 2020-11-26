#ベースイメージ
FROM php:7.4-fpm-buster

#option errorstop unreaderror x-errorlog
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

#composerをマルチステージビルドで導入
ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY --from=composer:1.10 /usr/bin/composer /usr/bin/composer

#拡張ライブラリ Laravel
RUN apt-get update && apt-get -y install \
  git \
  unzip \
  libzip-dev \
  libicu-dev \
  libonig-dev \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && docker-php-ext-install intl pdo_mysql \
  zip\
  bcmath

#php.iniの上書き
COPY ./php.ini /usr/local/etc/php/php.ini

WORKDIR /work
