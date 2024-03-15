FROM php:7.2.34-apache

# Установка необходимых пакетов для расширений и утилит
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libwebp-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libxpm-dev \
        libgmp-dev \
        libbz2-dev \
        libkrb5-dev \
        libicu-dev \
        libxml2-dev \
        libzip-dev \
        libcurl4-openssl-dev \
        libonig-dev \
        libssl-dev \
        libc-client-dev \
        libkrb5-dev \
        libpspell-dev \
        libtidy-dev \
        libenchant-dev \
        unixodbc-dev \
        libpq-dev \
        libsqlite3-dev \
        libldap2-dev \
        && ln -s /usr/lib/x86_64-linux-gnu/libldap.so /usr/lib/libldap.so \
        && ln -s /usr/lib/x86_64-linux-gnu/liblber.so /usr/lib/liblber.so

# Установка расширения GD для PHP 7.2
RUN docker-php-ext-install -j$(nproc) gd

# Установка остальных расширений PHP
RUN docker-php-ext-install -j$(nproc) bcmath bz2 exif gettext gmp mysqli soap sockets xmlrpc zip intl opcache pdo pdo_mysql pdo_pgsql pdo_sqlite

# Активация модулей mod_rewrite и mod_headers для Apache
RUN a2enmod rewrite headers

# Установка прав доступа для папок и файлов
RUN find /var/www/html/ -type d -exec chmod 775 {} \; \
    && find /var/www/html/ -type f -exec chmod 664 {} \; \
    && chown -R www-data:www-data /var/www/html/

# Открытие портов
EXPOSE 80