FROM php:7.4.15-apache
RUN echo 'ServerName localhost' >> /etc/apache2/apache2.conf
RUN service apache2 restart

# install dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libwebp-dev \
    curl \
    libcurl4 \
    libcurl4-openssl-dev \
    zlib1g-dev \
    libicu-dev \
    libmemcached-dev \
    memcached \
    default-mysql-client \
    libmagickwand-dev \
    unzip \
    libzip-dev \
    zip \
    nano && \
    rm -rf /var/lib/apt/lists/*
# memcached
RUN pecl install memcached-3.1.5
RUN docker-php-ext-enable memcached

# mcrypt
RUN pecl install mcrypt-1.0.3
RUN docker-php-ext-enable mcrypt

RUN apt-get update

RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp
RUN cd /usr/src/php/ext/gd && make
RUN cp /usr/src/php/ext/gd/modules/gd.so /usr/local/lib/php/extensions/no-debug-non-zts-20190902/gd.so
RUN docker-php-ext-install -j$(nproc) gd

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install intl
RUN docker-php-ext-install opcache
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.20

RUN apt-get update
RUN a2enmod rewrite
RUN service apache2 restart

RUN composer global require drush/drush
#RUN export PATH="\$HOME/.composer/vendor/drush/drush:\$PATH"
RUN composer create-project drupal/recommended-project:9.1.4 .
RUN cp web/sites/default/default.settings.php web/sites/default/settings.php && mkdir web/sites/default/files && chmod -R 777 web/sites/default/files/ && chmod 666 web/sites/default/settings.php


