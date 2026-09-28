FROM php:8.5-fpm-bookworm

RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        git \
        pkg-config \
        unzip \
        libicu-dev \
        libzip-dev; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

RUN set -eux; docker-php-ext-install -j"$(nproc)" pdo_mysql
RUN set -eux; docker-php-ext-install -j"$(nproc)" zip
RUN set -eux; docker-php-ext-install -j"$(nproc)" intl

RUN git config --system --add safe.directory /var/www/app

COPY --from=composer:2 /usr/bin/composer /usr/bin/composer
WORKDIR /var/www/app
