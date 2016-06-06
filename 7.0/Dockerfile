FROM php:7.0

RUN apt-get update -qq \
    && apt-get install -y -qq git wget pandoc ant texlive-fonts-recommended \
       libxslt-dev libzip-dev texlive-latex-recommended \
    && rm -rf /var/lib/apt/lists/*

RUN yes | pecl install xdebug && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini

RUN docker-php-ext-install xsl zip
RUN docker-php-ext-enable xdebug

# Grab a composer
RUN mkdir -p /opt/composer \
    && mkdir -p /opt/bin \
    && pushd /opt/composer \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === '070854512ef404f16bac87071a6db9fd9721da1684cd4589b1196c3faf71b9a2682e2311b36a5079825e155ac7ce150d') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && chmod +x /opt/composer/composer.phar
    && ln -s /opt/composer/composer.phar /opt/bin/composer

# Expand path to opt
ENV PATH /opt/bin:$PATH
