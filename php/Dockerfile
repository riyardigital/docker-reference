FROM php:8.2-fpm

# Install system dependencies & PHP extensions
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    zip \
    unzip \
    git \
    curl \
 && docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd \
 && rm -rf /var/lib/apt/lists/*

# Install Composer (from official image)
COPY --from=composer:2 /usr/bin/composer /usr/bin/composer

# Create non-root user (matching PUID/PGID)
ARG PUID=1000
ARG PGID=1000

RUN groupadd -g ${PGID} appgroup \
 && useradd -u ${PUID} -g appgroup -m appuser

# Working directory for the app
WORKDIR /var/www/html

# Copy custom php.ini configuration
COPY php.ini /usr/local/etc/php/conf.d/zz-custom.ini

# Make sure the directory exists and owned by appuser
RUN mkdir -p /var/www/html \
 && chown -R appuser:appgroup /var/www

# Switch to non-root user
USER appuser

EXPOSE 9000
CMD ["php-fpm"]
