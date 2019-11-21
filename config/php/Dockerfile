FROM php:7.3-fpm

WORKDIR /var/www

# nodejs sourse
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -

# Instal dependencies
RUN apt-get update -q && apt-get install -yqq \
    nodejs \
    git \
    curl \
    libzip-dev \
    unzip

# Clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# Install extensions
RUN docker-php-ext-install mbstring exif pdo pdo_mysql zip
# RUN docker-php-ext-configure gd --with-gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/
# RUN docker-php-ext-install gd

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Add user for laravel application
RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www
USER www

# RUN composer create-project laravel/laravel project

EXPOSE 9000
CMD [ "php-fpm" ]
