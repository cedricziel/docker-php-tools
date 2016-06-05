FROM php:7.0

RUN apt-get update -qq \
    && apt-get install -y -qq wget pandoc ant texlive-fonts-recommended \
       libxslt-dev texlive-latex-recommended \
    && rm -rf /var/lib/apt/lists/*
