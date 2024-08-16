# Gunakan image bitnami/laravel sebagai base image
FROM bitnami/laravel:latest

# Install dependencies tambahan yang diperlukan
USER root
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Set working directory
WORKDIR /app

# Salin file aplikasi Laravel ke dalam container
COPY . .

# Install dependencies Laravel
RUN composer install --no-dev --optimize-autoloader

# Generate key Laravel
RUN php artisan key:generate

# Set permissions
RUN chown -R bitnami:bitnami /app \
    && chmod -R 755 /app/storage

# Expose port
EXPOSE 8000

# Jalankan server Laravel
CMD ["php", "artisan", "serve", "--host", "0.0.0.0", "--port", "8000"]
