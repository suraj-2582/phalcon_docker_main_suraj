FROM php:8.2-fpm

RUN buildDeps="libxml2-dev zlib1g-dev" \
    && apt-get update -y \
    && apt install libzip4 libgd3 -y \
    && apt-get install wget curl libzip-dev libpng-dev libonig-dev -y \
    && apt-get install -y $buildDeps unzip git gnupg dirmngr --no-install-recommends --no-install-suggests \
    && pecl install redis psr \
    && docker-php-ext-enable redis psr \
    && docker-php-ext-install opcache soap \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get upgrade -y \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps

ENV PHALCON_VERSION=5.2.1
RUN curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz \
    && tar xzf v${PHALCON_VERSION}.tar.gz \
    && docker-php-ext-install ${PWD}/cphalcon-${PHALCON_VERSION}/build/phalcon \
    && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION}
    
RUN apt-get update -y
RUN pecl install xdebug
RUN  docker-php-ext-enable xdebug

RUN echo "session.save_path=\"/app/tmp\"" >> "$PHP_INI_DIR/php.ini"
RUN apt-get update
RUN apt-get install -y libcurl4-openssl-dev ssh nano pkg-config libssl-dev
RUN pecl install mongodb-1.17.2 && docker-php-ext-enable mongodb
RUN docker-php-ext-configure pcntl --enable-pcntl
RUN docker-php-ext-install pcntl
RUN apt-get upgrade -y
