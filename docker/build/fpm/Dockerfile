#FROM php:7.1-fpm
FROM laravel:php-fpm

# updates
RUN apt-get update && apt-get install -y libmcrypt-dev libicu-dev mysql-client libxml2-dev libssl-dev libpq-dev libbz2-dev libpng-dev \
  && rm -r /var/lib/apt/lists/* \
  && docker-php-ext-install \
    opcache \
    zip \
    bz2 \
    iconv \
    calendar \
    intl \
    dom \
    gd \
    mbstring \
    mcrypt \
    pcntl \
    mysqli \
    pdo \
    pdo_mysql \
    pdo_pgsql

# xdebug
ARG XDEBUG_ON=false
ARG XDEBUG_REMOTE_HOST=127.0.0.1
RUN if [ ${XDEBUG_ON} = true ]; then \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    echo "xdebug.default_enable = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_enable = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_autostart = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_connect_back = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.profiler_enable = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_host = ${XDEBUG_REMOTE_HOST}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.remote_port = 9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
;fi

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# install phpunit
RUN curl https://phar.phpunit.de/phpunit.phar -L > phpunit.phar \
    && chmod +x phpunit.phar \
    && mv phpunit.phar /usr/local/bin/phpunit \
    && phpunit --version

# install cron
RUN apt-get update && apt-get -y install rsyslog

# Change uid and gid of apache to docker user uid/gid
#RUN usermod -u 1000 www-data && groupmod -g 1000 www-data

# mark volume/s as externally mounted
VOLUME ["/var/www"]

# starting point
WORKDIR /var/www

# make web server connect to this port
EXPOSE 9000

CMD ["php-fpm"]