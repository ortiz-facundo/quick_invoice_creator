FROM php:8.2-apache

RUN chown -R www-data:www-data /srv/app \
    && a2enmod rewrite

# PHP and apache copy config
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY .docker/php.ini /usr/local/etc/php/php.ini
COPY .docker/vhost.conf /etc/apache2/sites-enabled/000-default.conf