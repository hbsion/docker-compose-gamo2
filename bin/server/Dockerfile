FROM webdevops/base-app:centos-7

ENV WEB_DOCUMENT_ROOT=/app \
    WEB_DOCUMENT_INDEX=index.php \
    WEB_ALIAS_DOMAIN=*.vm \
    WEB_PHP_TIMEOUT=600 \
    WEB_PHP_SOCKET=""

COPY conf/ /opt/docker/

RUN set -x \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
    && yum-install \
        ImageMagick \
        GraphicsMagick \
        jpegoptim \
        libjpeg-turbo-utils \
        optipng \
        pngcrush \
        pngnq \
        pngquant \
        # Install php (cli/fpm)
        php71w-cli \
        php71w-fpm \
        php71w-common \
        php71w-intl \
        php71w-imap \
        php71w-mysqlnd \
        php71w-pecl-memcached \
        php71w-mcrypt \
        php71w-gd \
        php71w-pgsql \
        php71w-mbstring \
        php71w-bcmath \
        php71w-soap \
        php71w-pecl-apcu \
        sqlite \
        php71w-xmlrpc \
        php71w-xml \
        geoip \
        php71w-ldap \
        ImageMagick-devel \
        ImageMagick-perl \
        php71w-pear \
        php71w-devel \
        gcc \
        make \
        php71w-opcache \
        php71w-pecl-imagick \
        php71w-pecl-mongodb \
        php71w-json \
        php71w-zip
        
RUN pecl channel-update pecl.php.net \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && pecl install redis \
    && echo "extension=redis.so" > /etc/php.d/redis.ini \
    && yum remove -y ImageMagick-devel php71w-devel gcc make
    # # Enable php services
    # && docker-service enable syslog \
    # && docker-service enable cron \
    # && docker-run-bootstrap \
    # && docker-image-cleanup

EXPOSE 80
EXPOSE 443