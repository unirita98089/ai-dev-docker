FROM php:8.1-fpm

# Install PDO MySQL extension
RUN docker-php-ext-install pdo_mysql

# Copy Composer binary from the Composer image
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html