FROM php:8.1-apache

# Update
RUN apt-get update --fix-missing && \
    apt-get upgrade -y && \
    apt-get --no-install-recommends install -y apt-utils && \
    rm -rf /var/lib/apt/lists/*

# Install stuff
RUN apt-get -y update && \
    apt-get -y --no-install-recommends install nano wget iproute2 && \
    apt-get -y --no-install-recommends install default-mysql-client zlib1g-dev libzip-dev libicu-dev && \
    apt-get -y --no-install-recommends install --fix-missing libpcre3-dev libmemcached-dev && \
    apt-get -y --no-install-recommends install --fix-missing apt-utils build-essential git curl libonig-dev && \
    apt-get -y --no-install-recommends install --fix-missing libcurl4 libcurl4-openssl-dev zip openssl && \
    rm -rf /var/lib/apt/lists/* && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install PHP extensions
RUN docker-php-ext-configure pdo_mysql --with-pdo-mysql=mysqlnd && \
    docker-php-ext-install pdo_mysql && \
    docker-php-ext-install zip && \
    docker-php-ext-install -j$(nproc) intl && \
    docker-php-ext-install bcmath && \
    docker-php-ext-install gettext && \
    docker-php-ext-install calendar && \
    docker-php-ext-install exif && \
    docker-php-ext-install opcache && \
    pecl install xdebug-3.1.3 && \
    pecl install memcached-3.1.5 && \
	pecl install redis-5.3.7 && \
	pecl install apcu-5.1.21 && \
    docker-php-ext-enable xdebug memcached redis apcu

# Setup apache
COPY start-apache /usr/local/bin
RUN a2enmod headers rewrite
RUN chown -R www-data:www-data /var/www
CMD ["start-apache"]