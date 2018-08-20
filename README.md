# PHP Test Runner

A phpunit + xdebug container.

## Supported tags and respective Dockerfile links

- `php7.1-fpm-alpine` `php7.1` `latest` [(php7.1/fpm-alpine/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.1/fpm-alpine/Dockerfile)
- `php7.1-apache` [(php7.1/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.1/apache/Dockerfile)
- `php7.0-fpm-alpine` `php7.0` [(php7.0/fpm-alpine/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.0/fpm-alpine/Dockerfile)
- `php7.0-apache` [(php7.0/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.0/apache/Dockerfile)
- `php5.6-fpm-alpine` `php5.6` [(php5.6/fpm-alpine/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php5.6/fpm-alpine/Dockerfile)
- `php5.6-apache` [(php5.6/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php5.6/apache/Dockerfile)

## What does it come with?

- phpunit
- xdebug
- composer
- bash
- sed
- git
- subversion
- mysql-client

## How to use this image

### Using it with `docker run`

Run phpunit tests

```
$ docker run -v $(pwd):/var/www/html --rm bostonuniversity/php-test-runner
```

Get phpunit version

```
$ docker run -v $(pwd):/var/www/html --rm bostonuniversity/php-test-runner phpunit --version
```

Open shell in container

```
$ docker run -v $(pwd):/var/www/html --rm -it bostonuniversity/php-test-runner bash
```

### Using it with `docker-compose run`

Example docker-compose.yml file:

```yaml
version: "3.7"
services:
  php-app:
    build: .
    volumes:
      - .:/var/www/html

  php-test-runner:
    image: bostonuniversity/php-test-runner
    volumes:
      - .:/var/www/html
```

To execute the tests, run `docker-compose run --rm php-test-runner`.

### Xdebug - Remote Debugging

Xdebug is configured with the following settings:

- `xdebug.remote_enable=1`
- `xdebug.remote_autostart=1`
- `xdebug.remote_host="host.docker.internal"`
- `xdebug.remote_port="9000"`
- `xdebug.remote_log="/var/log/xdebug.log"`

You can set/override any setting by providing a `XDEBUG_CONFIG` environment variable like so:

```
$ docker run -e XDEBUG_CONFIG="remote_host=192.168.65.2 remote_port=8999" -v $(pwd):/var/www/html --rm bostonuniversity/php-test-runner
```

Note: As of August 2018 `host.docker.internal` will work with Docker for Mac and Docker for Windows. However, it still does not seem to be supported on Docker for Linux. See this github issue for more information regarding linux: https://github.com/docker/for-linux/issues/264

## License

This project is licensed under the MIT License - see the [LICENSE](https://github.com/bu-ist/php-test-runner/blob/master/LICENSE) file for details.
