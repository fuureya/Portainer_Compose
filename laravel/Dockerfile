FROM php:8.4-fpm-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

#USER root

RUN apk add --no-cache \
    nano \
    bash \
    git \
    curl \
    zip \
    unzip \
    libpng \
    libpng-dev \
    libjpeg-turbo \
    libjpeg-turbo-dev \
    freetype \
    freetype-dev \
    libxml2-dev \
    libzip-dev \
    icu-dev \
    oniguruma-dev \
    nodejs \
    npm

RUN sed -i 's/^listen = .*/listen = 9990/' /usr/local/etc/php-fpm.d/www.conf

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html/

COPY ./app /var/www/html/

RUN composer install --no-dev --optimize-autoloader

EXPOSE 9990

CMD ["php-fpm"]
