[![](https://images.microbadger.com/badges/image/herloct/composer.svg)](http://microbadger.com/images/herloct/composer "Get your own image badge on microbadger.com")

## Supported tags and respective `Dockerfile` links

* [`PHP 7.0.11`, `latest`](https://github.com/herloct/docker-composer/blob/master/7.0.11/Dockerfile)
* [`PHP 5.6.26`](https://github.com/herloct/docker-composer/blob/master/5.6.26/Dockerfile)

## What is Composer?

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

> (https://getcomposer.org/doc/00-intro.md)

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
    -v /local/storages/composer:/composer \
    herloct/composer install --ignore-platform-reqs
```
