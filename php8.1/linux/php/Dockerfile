FROM php:8.1-fpm-alpine

RUN apk add -U --no-cache \
    bash \
    git \
    curl-dev \
    zip \
    libzip-dev \
    unzip \
    supervisor

RUN docker-php-ext-install pdo\
    pdo_mysql \
    mysqli \
    curl \
    zip \
    bcmath \
    pcntl

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

RUN apk add -U freetype-dev \
  libjpeg-turbo-dev \
  libpng-dev \
  libwebp-dev

RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j$(nproc) gd

RUN touch /var/run/supervisor.sock
COPY supervisord.conf /etc/supervisord.conf
RUN chmod 777 /etc/supervisord.conf
COPY docker-php-entrypoint-override /usr/local/bin/docker-php-entrypoint-override
RUN chmod 777 /usr/local/bin/docker-php-entrypoint-override
ENTRYPOINT ["/usr/local/bin/docker-php-entrypoint-override"]

USER 1000:1000
