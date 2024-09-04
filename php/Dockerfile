# Usa la imagen base de PHP 8.0 con FPM
FROM php:8.0-fpm

# Actualiza e instala dependencias necesarias
RUN apt update && apt install -y \
        zlib1g-dev \
        g++ \
        git \
        libicu-dev \
        zip \
        libzip-dev \
        libpng-dev \
        libjpeg-dev \
        libfreetype6-dev \
    && docker-php-ext-install \
        intl \
        opcache \
        pdo \
        pdo_mysql \
        gd \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

# Configura el directorio de trabajo para Laravel
WORKDIR /var/www

# Instala Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Instala Laravel (esto puede hacerse en un paso separado cuando se construya la imagen)
# Si estás copiando tu código desde el contexto de construcción, puedes omitir esta parte
# RUN composer create-project --prefer-dist laravel/laravel .

RUN composer global require laravel/installer

# Configura Git
RUN git config --global user.email "jeroalbusto00@gmail.com" \
    && git config --global user.name "jerodev"

