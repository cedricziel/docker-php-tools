FROM php:7.0

RUN apt-get update -qq \
    && apt-get install -y -qq git wget pandoc ant texlive-fonts-recommended \
       libxslt-dev libzip-dev texlive-latex-recommended \
    && rm -rf /var/lib/apt/lists/*

RUN yes | pecl install xdebug && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini

RUN docker-php-ext-install xsl zip
RUN docker-php-ext-enable xdebug
