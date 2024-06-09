# Use the official PHP image as a base
FROM php:8.3.8-bookworm

# Install necessary dependencies
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zip \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    libonig-dev \
    libxml2-dev \
    libzip-dev \
    curl \
    gnupg \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd mbstring pdo pdo_mysql zip bcmath

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Install Node.js and npm
RUN curl -fsSL https://deb.nodesource.com/setup_20.x | bash - && \
    apt-get install -y nodejs

RUN echo "which php" && which php && php -v && echo "which composer" && which composer && composer -V && echo "which node" && which node && node -v && echo "which npm" && which npm && npm -v


# Set working directory
WORKDIR /workspace

# Expose port 9000 and start php-fpm server
EXPOSE 9000
CMD ["php"]
