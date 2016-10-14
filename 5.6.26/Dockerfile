FROM php:5.6.26-alpine

MAINTAINER herloct <herloct@gmail.com>

RUN apk update --no-cache \
    && apk add --no-cache \
        git \
        openssl \
        su-exec

RUN mkdir -p /project /composer

ENV COMPOSER_HOME /composer

COPY install-composer.sh /usr/local/bin/install-composer.sh

RUN cd /tmp \
    && install-composer.sh \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

ENV PATH $COMPOSER_HOME/vendor/bin:$PATH

VOLUME ["/project", "/composer"]
WORKDIR /project

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh", "composer"]
CMD ["--version"]
