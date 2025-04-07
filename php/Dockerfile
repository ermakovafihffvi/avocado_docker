# php/Dockerfile
FROM php:8.2-fpm

# Copy composer.lock and composer.json into the working directory
COPY composer.lock composer.json /var/www/html/

# Set working directory
WORKDIR /var/www/html/

# Установка зависимостей
RUN apt-get update && apt-get install -y \
    libzip-dev zip unzip curl \
    && docker-php-ext-install pdo pdo_mysql zip

# Установка Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy existing application directory contents to the working directory
COPY ./ /var/www/html

# Assign permissions of the working directory to the www-data user
RUN usermod -u 1000 www-data

# Expose port 9000 and start php-fpm server (for FastCGI Process Manager)
EXPOSE 9000