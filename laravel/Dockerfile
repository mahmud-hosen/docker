FROM node:alpine
COPY . /app
WORKDIR /app
CMD node app.js


# Use an official PHP runtime as the base image
FROM php:7.4-fpm

# Set the working directory in the container
WORKDIR /var/www/html

# Install system dependencies and PHP extensions
RUN apt-get update && \
    apt-get install -y libpng-dev libjpeg-dev libfreetype6-dev zip unzip git && \
    docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd pdo pdo_mysql

# Install Composer (PHP dependency manager)
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy your Laravel application files into the container
COPY . .

# Install Laravel dependencies using Composer
RUN composer install

# Expose port 9000 to connect to the PHP-FPM server
EXPOSE 9000

# Start the PHP-FPM server
CMD ["php-fpm"]
