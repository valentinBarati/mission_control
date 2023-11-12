FROM alpine:latest
# Install packages and remove default server definition
RUN apk --no-cache update && apk add wget
RUN apk --no-cache add  \
    php81 \
    php81-ctype \
    php81-curl \
    php81-dom \
    php81-exif \
    php81-fileinfo \
    php81-fpm \
    php81-gd \
    php81-gd \
    php81-intl \
    php81-iconv \
    php81-xsl \
    php81-mbstring \
    php81-mysqli \
    php81-opcache \
    php81-openssl \
    php81-pecl-imagick \
    php81-pecl-redis \
    php81-phar \
    php81-session \
    php81-simplexml \
    php81-soap \
    php81-xml \
    php81-xmlreader \
    php81-zip \
    php81-zlib \
    php81-pdo \
    php81-xmlwriter \
    php81-tokenizer \
    php81-pdo_mysql \
    php81-fpm \
    nginx \
    supervisor \
    curl \
    tzdata \
    htop \
    mysql-client \
    dcron \
    mc \
    zip \
    unzip \
    php81-zip \
    git \
    openssh

# Configure nginx
COPY config/nginx.conf /etc/nginx/nginx.conf

# Configure PHP-FPM
COPY config/fpm-pool.conf /etc/php81/php-fpm.d/www.conf
COPY config/php.ini /etc/php81/conf.d/custom.ini
#COPY config/.env /home/app/.env

# Install PHP tools
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && chmod +x wp-cli.phar && mv wp-cli.phar /usr/local/bin/wp
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php --install-dir=/usr/local/bin --filename=composer

# Configure supervisord
COPY config/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Let supervisord start nginx & php81-fpm
CMD /usr/bin/supervisord -c /etc/supervisor/conf.d/supervisord.conf

EXPOSE 80
