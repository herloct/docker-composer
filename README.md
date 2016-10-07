[Docker](http://www.docker.com/) image for [PHP Composer](https://getcomposer.org).

[![](https://images.microbadger.com/badges/image/herloct/composer.svg)](http://microbadger.com/images/herloct/composer "Get your own image badge on microbadger.com")

## What's Inside

This image is based on [official PHP 7.0 image](https://hub.docker.com/_/php/),
using Alpine Linux instead of Debian for smaller size.

## Supported tags and respective `Dockerfile` links

* [`1.2.1`, `latest`](https://github.com/herloct/docker-composer/blob/master/1.2.1/Dockerfile)

## How to use this image

Basic usage using current user id (uid).

```sh
docker run --rm \
    -e LOCAL_USER_ID=$(id -u) \
    -v /local/path:/project \
    herloct/composer [<options>]
```

**Remember to always add `--ignore-platform-reqs` for `install`, `require`, and `update` command, since this image
doesn't add any `ext-*` other than what php:7.*-alpine provides.**

For example, to install dependencies.

```sh
docker run --rm \
    -e LOCAL_USER_ID=$(id -u) \
    -v /local/path:/project \
    herloct/composer install --ignore-platform-reqs
```

If you want to cache composer for faster dependency install/update, just add volume to `/composer`.

```sh
docker run --rm \
    -e LOCAL_USER_ID=$(id -u) \
    -v /local/path:/project \
    -v /local/storages/composer:/composer \
    herloct/composer install --ignore-platform-reqs
```
