FROM php:7-fpm
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
COPY www.conf /usr/local/etc/php-fpm.d/
