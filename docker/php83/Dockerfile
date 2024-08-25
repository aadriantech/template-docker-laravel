FROM php:8.3-fpm-alpine

# Install system dependencies
RUN apk update && apk add --no-cache \
    bash \
    curl \
    libpng-dev \
    libzip-dev \
    zip \
    unzip

# Install PHP extensions
RUN docker-php-ext-install pdo pdo_mysql gd zip

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /var/www/html

# Copy the application files
COPY ./src /var/www/html/

# Copy the www.conf file to the PHP-FPM configuration directory
COPY /docker/php83/www.conf /usr/local/etc/php-fpm.d/www.conf

# Copy the entrypoint script
COPY /docker/php83/entrypoint.sh /entrypoint.sh

# Make the entrypoint script executable
RUN chmod +x /entrypoint.sh

# Set proper permissions
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

# Switch to non-root user
USER www-data

# Expose the port
EXPOSE 9000

# Set the entrypoint
ENTRYPOINT ["/entrypoint.sh"]