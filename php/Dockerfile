ARG PHP_VERSION=""
FROM php:${PHP_VERSION:+${PHP_VERSION}-}fpm-alpine

RUN apk update; \
    apk upgrade;

RUN apk --no-cache add linux-headers pcre-dev ${PHPIZE_DEPS} \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug \
  && apk del pcre-dev ${PHPIZE_DEPS}

# bump up the number of allowed child processes for debugging
RUN sed -i '/^pm.max_children/s/.*/pm.max_children = 30/' /usr/local/etc/php-fpm.d/www.conf
