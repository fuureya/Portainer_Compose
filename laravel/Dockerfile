FROM php:8.4-fpm-alpine

ENV COMPOSER_ALLOW_SUPERUSER=1 \
    COMPOSER_HOME=/composer

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

RUN docker-php-ext-configure gd \
        --with-freetype=/usr/include/ \
        --with-jpeg=/usr/include/ \
    && docker-php-ext-install \
        gd \
        pdo \
        pdo_mysql \
        zip \
        intl \
        mbstring \
        xml

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html/

COPY ./app /var/www/html/

RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

RUN composer install 

EXPOSE 9990

CMD ["php-fpm"]
