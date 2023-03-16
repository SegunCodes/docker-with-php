FROM php:8.1-fpm-alpine

RUN docker-php-ext-install pdo pdo_mysql

#ALLOW SUPER USER
ENV COMPOSER_ALLOW_SUPERUSER=1

#Obtain composer using multu-stage build
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/composer

#copy only composer.json and composer.lock
#this is enough to take advantage of docker cache and composer install will be executed
#only when composer.json or composer.lock have changed
COPY ./app/composer.* ./

#install
RUN composer install --prefer-dist --no-dev --no-scripts --no-progress --no-interaction

#copy application files to working directory
COPY ./app .

#run composer dump-autoload --optimize
RUN composer dump-autoload --optimize