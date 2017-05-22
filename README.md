[![license](https://img.shields.io/github/license/herloct/docker-composer.svg)]()
[![Build Status](https://travis-ci.org/herloct/docker-composer.svg?branch=master)](https://travis-ci.org/herloct/docker-composer)

## Supported tags and respective `Dockerfile` links

* Composer 1.4.2 + PHP 7.1.5: [`1.4.2-php7.1`, `latest`](https://github.com/herloct/docker-composer/blob/1.4.2/7.1/Dockerfile)
* Composer 1.4.2 + PHP 7.0.19: [`1.4.2-php7.0`](https://github.com/herloct/docker-composer/blob/1.4.2/7.0/Dockerfile)
* Composer 1.4.2 + PHP 5.6.30: [`1.4.2-php5.6`](https://github.com/herloct/docker-composer/blob/1.4.2/5.6/Dockerfile)

## What is Composer?

Composer is a tool for dependency management in PHP. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

> https://getcomposer.org/doc/00-intro.md

## Is it better than [official Composer images](https://hub.docker.com/r/_/composer/)?

I'm using official image's script as reference, and major PHP versions (5.6, 7.0, and 7.1) as Base Image.
This image also use [hirak/prestissimo](https://github.com/hirak/prestissimo) for faster downloads.

## How to use this image

Basic usage using current user.

```sh
docker run --rm \
    --user $(id -u):$(id -g) \
    --volume /local/path:/project \
    herloct/composer[:tag] [<options>]
```

> **Remember to add `--ignore-platform-reqs` for `install`, `require`, and `update` command, since this image
doesn't add any `ext-*` other than what php:*-alpine provides.**

For example, to install dependencies.

```sh
docker run --rm \
    --user $(id -u):$(id -g) \
    --volume /local/path:/project \
    herloct/composer install --ignore-platform-reqs
```

If you want to cache composer for faster install/update, just add volume to `/composer/cache`.

```sh
docker run --rm \
    --user $(id -u):$(id -g) \
    --volume /local/path:/project \
    --volume /local/composer:/composer/cache \
    herloct/composer install --ignore-platform-reqs
```

## Volumes

* `/project`: Your PHP project directory.
* `/composer/cache`: Composer cache directory.
