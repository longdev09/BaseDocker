# Sử dụng hình ảnh chứa PHP và Apache
FROM php:8.0-apache

# Cài đặt các gói phụ thuộc của Laravel
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

# Cài đặt Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Đặt thư mục làm việc
WORKDIR /var/www/html

# Sao chép mã nguồn Laravel vào container
COPY . .

# Cài đặt các gói Composer
RUN composer install

# Phục cấu hình Apache để trỏ vào thư mục public của Laravel
RUN sed -i -e 's/html/html\/public/g' /etc/apache2/sites-available/000-default.conf

# Kích hoạt module rewrite của Apache
RUN a2enmod rewrite

# Khởi động Apache
CMD ["apache2-foreground"]
