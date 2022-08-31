FROM php:8.1-apache

RUN apt update
RUN apt install -y \
    vim \
    g++ \
    libicu-dev \
    libpq-dev \
    libzip-dev \
    zip \
    zlib1g-dev \
    nodejs \
    npm \
    tzdata \
    libonig-dev

RUN docker-php-ext-install pdo_mysql mysqli mbstring

RUN a2enmod rewrite

RUN sed -i -e 's#DocumentRoot /var/www/html#DocumentRoot /var/www/html/public#' /etc/apache2/sites-available/000-default.conf

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && mv composer.phar /usr/local/bin/composer

RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash -
RUN apt-get install -y nodejs

WORKDIR /var/www/html

RUN composer global require "laravel/installer"
