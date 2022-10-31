FROM php:8.1-apache

RUN curl https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    chmod +x /usr/local/bin/composer

RUN apt-get update && apt-get install -y git zlib1g-dev libzip-dev

RUN yes | pecl install xdebug

RUN docker-php-ext-install zip pdo pdo_mysql  && \
       docker-php-ext-enable zip pdo pdo_mysql xdebug
