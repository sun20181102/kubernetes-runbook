FROM centos:7

ENV HTTPD_VERSION 2.4
ENV PHP_VERSION 56u

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y https://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    #yum makecache && yum update -y; \
    yum install -y --enablerepo=remi-php80 \
        httpd \
        php80-php \
        php80-php-bcmath \
        php80-php-cli \
        php80-php-common \
        php80-php-gd \
        php80-php-intl \
        php80-php-mbstring \
        php80-php-mcrypt \
        php80-php-mysqlnd \
        php80-php-opcache \
        php80-php-pdo \
        php80-php-pear \
        php80-php-pecl-igbinary \
        php80-php-pecl-jsonc \
        php80-php-pecl-redis \
        php80-php-process \
        php80-php-xml \
        php80-php-xmlrpc \
    && \
    rm -rf /var/lib/yum/ && \
    rm -rf /var/cache/ && \
    #rm -rf /etc/httpd/conf.d/* && \
    mkdir /var/www/html/default && \
    echo "xXx" > /var/www/html/default/index.html && \
    ln -s /usr/bin/php80 /usr/bin/php && \
# Modify PHP configuration parameters
    sed -i 's/;date.timezone =/date.timezone = "Asia\/Kuala_Lumpur"/g' /etc/opt/remi/php80/php.ini && \
    sed -i 's/short_open_tag = Off/short_open_tag = On/g' /etc/opt/remi/php80/php.ini && \
    sed -i 's/;error_log = syslog/error_log = syslog/g' /etc/opt/remi/php80/php.ini && \
    sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /etc/opt/remi/php80/php.ini && \
    sed -i 's/;opcache.enable_cli=0/opcache.enable_cli=0/' /etc/opt/remi/php80/php.d/10-opcache.ini && \
    sed -i 's/;opcache.validate_timestamps=1/opcache.validate_timestamps=1/' /etc/opt/remi/php80/php.d/10-opcache.ini && \
    sed -i 's/opcache.memory_consumption=128/opcache.memory_consumption=512/' /etc/opt/remi/php80/php.d/10-opcache.ini && \
    sed -i 's/;opcache.revalidate_freq=2/opcache.revalidate_freq=30/' /etc/opt/remi/php80/php.d/10-opcache.ini && \
    sed -i 's/;always_populate_raw_post_data = -1/always_populate_raw_post_data = -1/g' /etc/opt/remi/php80/php.ini && \
    httpd -v && \
    php -v

COPY httpd.conf /etc/httpd/conf/httpd.conf
COPY default.conf /etc/httpd/conf.d/default.conf
WORKDIR /var/www/html/

EXPOSE 80
CMD ["httpd", "-DFOREGROUND"]