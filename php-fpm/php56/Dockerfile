FROM php:5.6-fpm

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
        redis \
        mcrypt\
        xdebug

#  Install Composer
ENV COMPOSER_HOME /root/composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.10.20
ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /var/www

#  Write Permission
RUN usermod -u 1000 www-data

EXPOSE 9056
