FROM php:7.3.6-fpm

COPY php.ini /usr/local/etc/php
WORKDIR /var/www/html

RUN apt-get update && \
    apt-get install git -y && \
    apt-get install zip -y && \
    apt-get install libzip-dev -y

RUN apt-get update
RUN apt-get install -y libxslt-dev libxml2-dev libpam-dev libedit-dev
RUN apt-get install --no-install-recommends -y libpq-dev
RUN docker-php-ext-install pdo pgsql pdo_pgsql zip
RUN apt-get update && apt-get -y install cron

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN apt-get install iputils-ping -y
RUN apt-get install -y vim git

# Install Xdebug
#RUN pecl install redis-4.0.1 \
#    && pecl install xdebug-2.6.0 \
#    && docker-php-ext-enable redis xdebug

# Code sniffer
ENV PHPCS_VERSION=3.3.2
RUN curl -L https://github.com/squizlabs/PHP_CodeSniffer/releases/download/$PHPCS_VERSION/phpcs.phar > /usr/local/bin/phpcs \
    && chmod +x /usr/local/bin/phpcs \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*
