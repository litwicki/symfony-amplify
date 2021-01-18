FROM php:fpm-8.0

WORKDIR /var/www/html

COPY . .

RUN apk --update --no-cache add git

RUN apt-get update \
 && apt-get install -y git \
 libicu-dev \
 libcurl4-gnutls-dev \
 libmcrypt-dev \
 bzip2 \
 libbz2-dev \
 zlib1g-dev \
 g++ \
 libxml2-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install -j$(nproc) intl \
    && docker-php-ext-install -j$(nproc) curl \
    && docker-php-ext-install -j$(nproc) bz2 \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) pdo_mysql \
    && docker-php-ext-install -j$(nproc) mysqli \
    && docker-php-ext-install -j$(nproc) zip \
    && docker-php-ext-install -j$(nproc) mcrypt \
    && docker-php-ext-install -j$(nproc) opcache

# Enable and configure xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
	php /usr/local/bin/composer self-update

RUN usermod -u 1000 www-data

CMD composer install

EXPOSE 9000