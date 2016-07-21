FROM php:5.5

RUN apt-get update && apt-get install --no-install-recommends --no-install-suggests -y \
    zlib1g-dev \
    && rm -r /var/lib/apt/lists/*

# Install Extensions
RUN docker-php-ext-install zip

# Install Pecl Extensions
RUN pecl install xdebug-2.4.0 && \
    echo "zend_extension=/usr/local/lib/php/extensions/no-debug-non-zts-20121212/xdebug.so" > /usr/local/etc/php/conf.d/xdebug.ini

# Install Composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" \
    mv composer.phar /usr/local/bin/composer