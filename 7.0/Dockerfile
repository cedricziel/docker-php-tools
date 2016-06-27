FROM php:7.0

RUN apt-get update -qq \
    && apt-get install -y -qq git wget pandoc ant texlive-fonts-recommended \
       libxslt-dev libzip-dev texlive-latex-recommended \
       libfreetype6-dev libjpeg62-turbo-dev libmcrypt-dev libpng12-dev \
    && rm -rf /var/lib/apt/lists/*

RUN yes | pecl install xdebug && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini

RUN docker-php-ext-install -j$(nproc) xsl zip iconv mcrypt pdo_mysql exif pcntl
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-enable xdebug

# Grab a composer
RUN mkdir -p /opt/composer \
    && mkdir -p /opt/bin \
    && cd /opt/composer \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === 'e115a8dc7871f15d853148a7fbac7da27d6c0030b848d9b3dc09e2a0388afed865e6a3d6b3c0fad45c48e2b5fc1196ae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php');" \
    && chmod +x /opt/composer/composer.phar \
    && ln -s /opt/composer/composer.phar /opt/bin/composer \
    && cd /

# Expand path to opt
ENV PATH /opt/bin:$PATH

# Disable interactive prompts with gcloud
ENV CLOUDSDK_CORE_DISABLE_PROMPTS 1

# Install Google Cloud SDK
RUN echo "deb http://packages.cloud.google.com/apt cloud-sdk-jessie main" | tee /etc/apt/sources.list.d/google-cloud-sdk.list \
    && curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - \
    && apt-get update -qq \
    && apt-get install -y -qq google-cloud-sdk \
    && rm -rf /var/lib/apt/lists/*
