FROM php:8.0-fpm-alpine

ENV TZ=Asia/Shanghai

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

# Libs
# RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
#     apk update && \
#     apk add --no-cache make \
#                        libc-dev \
#                        gcc \
#                        g++ \
#                        linux-headers \
#                        wget \
#                        tzdata \
#                        libxml2-dev \
#                        openssl-dev \
#                        sqlite-dev \
#                        curl-dev \
#                        oniguruma-dev \
#                        autoconf \
#                        libzip-dev \
#                        freetype-dev \
#                        libjpeg-turbo-dev \
#                        libpng-dev \
#                        imagemagick \
#                        imagemagick-dev
# PHP-Extensions
RUN set -eux; \
    chmod +x /usr/local/bin/install-php-extensions; \
    install-php-extensions \
    amqp \
    bcmath \
    bz2 \
    calendar \
    decimal \
    enchant \
    event \
    exif \
    gd \
    gettext \
    gmp \
    igbinary \
    imagick \
    intl \
    lzf \
    memcached \
    mongodb \
    mysqli \
    opcache \
    pcntl \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    redis \
    sockets \
    swoole \
    tidy \
    timezonedb \
    uuid \
    xlswriter \
    xsl \
    yac \
    yaml \
    zip; \
    apk add --no-cache tzdata

# composer
RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');" && \
    composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ && \
    # Clean
    apk del && rm -rf /var/cache/apk/* && rm -rf /var/lib/apt/lists/*

WORKDIR /var/www/html

EXPOSE 9000

CMD ["php-fpm", "-R"]