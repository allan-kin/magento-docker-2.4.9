FROM php:8.5-fpm-bookworm

ARG COMPOSER_VERSION=2.10.0

RUN apt-get update && apt-get install -y --no-install-recommends \
    bash \
    git \
    unzip \
    zip \
    curl \
    nano \
    vim \
    cron \
    msmtp-mta \
    default-mysql-client \
    libicu-dev \
    libxml2-dev \
    libxslt1-dev \
    libzip-dev \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libwebp-dev \
    libonig-dev \
    libcurl4-openssl-dev \
    libsodium-dev \
    libssl-dev \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg \
    --with-webp

RUN docker-php-ext-install -j"$(nproc)" \
    bcmath \
    ftp \
    gd \
    intl \
    mbstring \
    pdo_mysql \
    soap \
    sockets \
    xsl \
    zip

RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php \
    && php /tmp/composer-setup.php \
        --version=${COMPOSER_VERSION} \
        --install-dir=/usr/local/bin \
        --filename=composer \
    && rm /tmp/composer-setup.php

COPY php.ini /usr/local/etc/php/conf.d/zz-magento.ini

ARG HOST_UID=1000
ARG HOST_GID=1000

RUN groupmod -o -g ${HOST_GID} www-data \
    && usermod -o -u ${HOST_UID} -g ${HOST_GID} www-data

RUN mkdir -p /tmp/composer-cache \
    && chown -R www-data:www-data /tmp/composer-cache

RUN ln -sf /usr/bin/msmtp /usr/sbin/sendmail

RUN printf "defaults\n\
auth off\n\
tls off\n\
logfile /tmp/msmtp.log\n\
account default\n\
host mailpit\n\
port 1025\n\
from admin@example.com\n" > /etc/msmtprc \
    && chmod 644 /etc/msmtprc \
    && ln -sf /usr/bin/msmtp /usr/sbin/sendmail

USER www-data

WORKDIR /var/www/html
