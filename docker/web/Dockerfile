FROM php:8.1-apache

# Install PHP PostgreSQL extensions
RUN apt-get update && apt-get install -y libpq-dev \
    && docker-php-ext-install pdo pdo_pgsql \
    && rm -rf /var/lib/apt/lists/*

# Remove default Apache files
RUN rm -rf /var/www/html/*

# Copy static web page
COPY docker/web/index.html /var/www/html/index.html

# Permissions
RUN chown -R www-data:www-data /var/www/html \
    && chmod -R 755 /var/www/html

EXPOSE 80
