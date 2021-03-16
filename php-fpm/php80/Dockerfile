FROM php:8.0-fpm

RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list \
    && sed -i 's/security.debian.org/mirrors.aliyun.com/' /etc/apt/sources.list

# Install Tools
RUN apt-get update && apt-get install -y \
        git \
        vim

# Install PHP Extentions
ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/
RUN chmod +x /usr/local/bin/install-php-extensions \
    && install-php-extensions gd \
        zip \
        pdo_mysql \
        mysqli \
        intl \
        gmp \
        redis \
        mongodb \
        apcu \
        xdebug

#  Install Composer
ENV COMPOSER_HOME /root/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

#  Write Permission
RUN usermod -u 1000 www-data

EXPOSE 9080
