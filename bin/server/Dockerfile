FROM webdevops/base-app:centos-7

ENV WEB_DOCUMENT_ROOT=/app \
    WEB_DOCUMENT_INDEX=index.php \
    WEB_ALIAS_DOMAIN=*.vm \
    WEB_PHP_TIMEOUT=600 \
    WEB_PHP_SOCKET=""

COPY conf/ /opt/docker/

RUN set -x \
    && rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
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
        php71-cli \
        php71-fpm \
        php71-common \
        php71-intl \
        php71-imap \
        php71-mysqlnd \
        php71-pecl-memcached \
        php71-mcrypt \
        php71-gd \
        php71-pgsql \
        php71-mbstring \
        php71-bcmath \
        php71-soap \
        php71-pecl-apcu \
        sqlite \
        php71-xmlrpc \
        php71-xml \
        geoip \
        php71-ldap \
        ImageMagick-devel \
        ImageMagick-perl \
        php71-pear \
        php71-devel \
        gcc \
        make \
        php71-opcache \
        php71-pecl-imagick \
        php71-pecl-mongodb \
    && pecl channel-update pecl.php.net \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer \
    && pecl install redis \
    && echo "extension=redis.so" > /etc/php.d/redis.ini \
    && yum remove -y ImageMagick-devel php71-devel gcc make \
    # Enable php services
    && docker-service enable syslog \
    && docker-service enable cron \
    && docker-run-bootstrap \
    && docker-image-cleanup