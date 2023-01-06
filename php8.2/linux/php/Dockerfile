FROM php:8.2.0RC6-fpm-alpine3.15

RUN apk add -U --no-cache \
    bash \
    git \
    curl-dev \
    zip \
    libzip-dev \
    unzip \
    php8-bcmath \
    php8-ctype \
    php8-curl \
    php8-dom \
    php8-fileinfo \
    php8-json \
    php8-mbstring \
    php8-openssl \
    php8-xml \
    php8-xmlreader \
    php8-xmlwriter \
    php8-zlib \
    supervisor

RUN docker-php-ext-install pdo\
    pdo_mysql \
    mysqli \
    curl \
    zip \
    bcmath

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apk add -U freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev \
  libwebp-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd

USER 1000:1000
