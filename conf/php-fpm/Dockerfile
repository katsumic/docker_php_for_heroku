FROM php:7.4.4-fpm-alpine
LABEL maintainer="katsumic"

ARG TZ

ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_NO_INTERACTION 1
ENV COMPOSER_HOME /composer

RUN set -eux && \
  apk update && \
  apk add --update --no-cache --virtual=.build-dependencies \
    autoconf \
    make \
    gcc \
    g++ \
    tzdata \
    git && \
  apk add --update --no-cache \
    libzip-dev \
    icu-dev \
    oniguruma-dev \
    curl-dev \
    postgresql-dev \
    nodejs \
    npm && \
  cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
  echo ${TZ} > /etc/timezone && \
  pecl install xdebug && \
  apk del .build-dependencies && \
  docker-php-ext-install \
    zip \
    intl \
    mbstring \
    bcmath \
    curl \
    pdo_pgsql && \
  docker-php-ext-enable xdebug && \
  curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer config -g repos.packagist composer https://packagist.jp && \
  composer global require hirak/prestissimo
