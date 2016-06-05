FROM php:7.0

RUN apt-get update -qq \
    && apt-get install -y -qq git wget pandoc ant texlive-fonts-recommended \
       libxslt-dev texlive-latex-recommended \
    && rm -rf /var/lib/apt/lists/*

RUN docker-php-ext-install xsl zip
