# Use an official PHP image with Apache
FROM php:8.2-apache

RUN a2enmod rewrite
 
RUN apt-get update \
  && apt-get install -y libzip-dev git wget --no-install-recommends \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
 
RUN docker-php-ext-install pdo mysqli pdo_mysql zip;
 
# TODO: composer is not working on the container, check it out
RUN wget https://getcomposer.org/download/2.0.9/composer.phar \
    && mv composer.phar /usr/bin/composer && chmod +x /usr/bin/composer


# PHP and apache copy config
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY .docker/php.ini /usr/local/etc/php/php.ini
COPY .docker/vhost.conf /etc/apache2/sites-enabled/000-default.conf

# Fix vlume mapping of vendor folder ommition (bc fixion long loading issues on Windows)
COPY vendor /var/www/html/vendor

WORKDIR /var/www/html