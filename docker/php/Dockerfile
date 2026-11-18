FROM php:8.4-fpm-alpine

# Extensions PHP nécessaires :
# pdo_mysql (Doctrine), intl (validation, formats), opcache (performances), zip (Composer)
RUN apk add --no-cache icu-dev libzip-dev \
    && docker-php-ext-install pdo_mysql intl opcache zip

# Composer, copié depuis son image officielle
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/api
