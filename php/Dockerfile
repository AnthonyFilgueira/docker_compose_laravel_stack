# Instalación de PHP en Ubuntu 22.04
FROM ubuntu:22.04

LABEL MAINTAINER="Anthony Filgueira"

ENV TZ=America/Lima

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update \
  && apt-get install -y locales \
  && locale-gen en_US.UTF-8

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8

RUN apt-get update \
  && apt-get install -y \
    curl \
    git \
    software-properties-common \
    unzip \
    zip \
  && add-apt-repository -y ppa:ondrej/php \
  && apt-get update \
  && apt-get install -y \
    php8.2-fpm \
    php8.2-cli \
    php8.2-curl \
    php8.2-fpm \
    php8.2-gd \
    php8.2-imap \
    php8.2-mbstring \
    php8.2-mysql \
    php8.2-pgsql \
    php8.2-xml \
    php-memcached \
  && php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
  && mkdir /run/php \
  && apt-get remove -y --purge software-properties-common \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY php-fpm.conf /etc/php/8.2/fpm/php-fpm.conf
COPY www.conf /etc/php/8.2/fpm/pool.d/www.conf

EXPOSE 9000
CMD ["php-fpm8.2"]