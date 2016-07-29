# docker-php-tools

Base Image for testing PHP applications with additional tools installed.

[The image on docker hub](https://hub.docker.com/r/cedricziel/docker-php-tools/)

## Interaction with a docker daemon

These images package the docker binaries from official sources, so you
can interact with a remote docker daemon.

```
~ $ DOCKER_HOST=tcp://docker:2375 docker info
```

## Pre-installed PHP extensions

* xdebug
* xsl
* zip
* iconv
* mcrypt
* pdo_mysql
* exif
* pcntl
* gd

## Installed Tools

### Build

* ant
* docker binaries

### Dependency Management

* composer

### Documentation

* pandoc
* texlive

### Packages

* libxslt-dev
* Google Cloud SDK

### Version control

* git

## License

MIT License
