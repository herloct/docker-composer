FROM php:5.6.30-alpine

MAINTAINER herloct <herloct@gmail.com>

ENV COMPOSER_VERSION=1.3.2 \
    COMPOSER_HOME=/composer \
    COMPOSER_ALLOW_SUPERUSER=1

COPY install-composer.sh /usr/local/bin/install-composer.sh

RUN apk update --no-cache \
    && apk add --no-cache \
        git \
        openssl \
        su-exec \

    && mkdir -p /project $COMPOSER_HOME \

    && ( \
        cd /tmp \
        && install-composer.sh \
        && rm /usr/local/bin/install-composer.sh \
    ) \

    && composer global require -a --prefer-dist "hirak/prestissimo:^0.3" \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

ENV PATH=$COMPOSER_HOME/vendor/bin:$PATH \
    COMPOSER_ALLOW_SUPERUSER=0

VOLUME ["/project", "$COMPOSER_HOME/cache"]
WORKDIR /project

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh", "composer"]
CMD ["--version"]
