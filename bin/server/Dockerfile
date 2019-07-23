FROM centos:latest

RUN yum update -y

# Install Apache
RUN yum install httpd httpd-tools -y
RUN yum -y install httpd; yum clean all; systemctl enable httpd.service


# Install PHP7.1
RUN yum install -y epel-release
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
RUN yum repolist

RUN yum install -y \
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
    && echo "extension=redis.so" > /etc/php.d/redis.ini


RUN chown -R apache:apache /var/www/html

WORKDIR /var/www/html

EXPOSE 80 443

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]