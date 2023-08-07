FROM php:8.2-fpm-alpine

# Устанавливаем зависимости
RUN apk add --no-cache \
        autoconf \
        g++ \
        imagemagick \
        imagemagick-dev \
        libtool \
        libgomp \
        make \
        pcre-dev \
        postgresql-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick \
    && docker-php-ext-install pdo pdo_mysql pdo_pgsql \
    && apk del g++ imagemagick-dev libtool make pcre-dev
# Установка Xdebug
RUN apk add --no-cache linux-headers \
	&& apk add --update --no-cache --virtual .build-dependencies $PHPIZE_DEPS\
	&& pecl install xdebug \
	&& docker-php-ext-enable xdebug \
	&& pecl clear-cache \
	&& apk del .build-dependencies

# Устанавливаем дополнительные инструменты
RUN apk add --no-cache \
        nano \
        bash \
 && apk update

WORKDIR /src