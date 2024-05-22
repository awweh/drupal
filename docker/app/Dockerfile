FROM php:5.6-fpm-alpine

ARG WWWGROUP=1000

WORKDIR /app

ENV DEBIAN_FRONTEND noninteractive
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apk add --no-cache --virtual .dd-build-deps libpng-dev freetype-dev libjpeg-turbo-dev postgresql-dev libxml2-dev libzip-dev oniguruma-dev $PHPIZE_DEPS \
   && docker-php-ext-install mbstring pdo_mysql pdo_pgsql zip \
   && docker-php-ext-install opcache bcmath

RUN apk add libxml2-dev libzip-dev \
    libpng-dev libwebp-dev libpng-dev libxpm-dev libssh-dev libmcrypt-dev \
    gcc make autoconf libc-dev

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN apk add mysql-client bash nginx net-tools vim gnupg curl ca-certificates htop sudo zip unzip git supervisor wget openssl

EXPOSE 80
EXPOSE 443

CMD ["/bin/bash", "-c", "php-fpm && nginx -g "daemon off;""]