FROM php:8.4-fpm-alpine

RUN apk add --no-cache \
    git \
    curl \
    libpng-dev \
    libxml2-dev \
    oniguruma-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libzip-dev \
    icu-dev \
    zip \
    unzip

RUN docker-php-ext-configure gd \
    --with-freetype \
    --with-jpeg

RUN docker-php-ext-install \
    # pdo \
    intl \
    mysqli \
    pdo_mysql \
    bcmath \
    # ctype \
    # fileinfo \
    # json \
    mbstring \
    gd \
    zip \
    exif \
    # tokenizer \
    xml

# install composer (best way)
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www

CMD ["php-fpm"]
