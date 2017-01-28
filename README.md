[![](https://images.microbadger.com/badges/image/herloct/composer.svg)](http://microbadger.com/images/herloct/composer "Get your own image badge on microbadger.com")

## Supported tags and respective `Dockerfile` links

* Composer 1.3.2 + PHP 7.1.1: [`1.3.2-php7.1`, `latest`](https://github.com/herloct/docker-composer/blob/1.3.2/7.1/Dockerfile)
* Composer 1.3.2 + PHP 7.0.15: [`1.3.2-php7.0`](https://github.com/herloct/docker-composer/blob/1.3.2/7.0/Dockerfile)
* Composer 1.3.2 + PHP 5.6.30: [`1.3.2-php5.6`](https://github.com/herloct/docker-composer/blob/1.3.2/5.6/Dockerfile)

## What is Composer?

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

> https://getcomposer.org/doc/00-intro.md

## How to use this image

Basic usage using current user id (uid).

```sh
docker run --rm \
    -e LOCAL_USER_ID=$(id -u) \
    -v /local/path:/project \
    herloct/composer [<options>]
```

> **Remember to always add `--ignore-platform-reqs` for `install`, `require`, and `update` command, since this image
doesn't add any `ext-*` other than what php:*-alpine provides.**

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
    -v /local/storages/composer:/composer/cache \
    herloct/composer install --ignore-platform-reqs
```

## Environment Variables

* **LOCAL_USER_ID**: User ID (UID) for container, so it could have same permission as host user.

## Volumes

* **/project**: Your PHP project directory.
* **/composer/cache**: Composer directory (cache, global dependencies, etc).
