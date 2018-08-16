# PHP Test Runner

[![Docker pull](https://img.shields.io/docker/pulls/bostonuniversity/php-test-runner.svg)](https://hub.docker.com/r/bostonuniversity/php-test-runner/) [![Docker stars](https://img.shields.io/docker/stars/bostonuniversity/php-test-runner.svg)](https://hub.docker.com/r/bostonuniversity/php-test-runner/) [![Github issues](https://img.shields.io/github/issues/bu-ist/php-test-runner.svg)](https://github.com/bu-ist/php-test-runner/issues) [![License](https://img.shields.io/github/license/bu-ist/php-test-runner.svg)](https://github.com/bu-ist/php-test-runner/blob/master/LICENSE)

A phpunit + xdebug container.

## Supported tags and respective Dockerfile links

- `php7.1` `latest` [(php7.1/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.1/apache/Dockerfile)
- `php7.1-apache` [(php7.1-apache/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.1-apache/apache/Dockerfile)
- `php7.0` [(php7.0/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.0/apache/Dockerfile)
- `php7.0-apache` [(php7.0-apache/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php7.0-apache/apache/Dockerfile)
- `php5.6` [(php5.6/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php5.6/apache/Dockerfile)
- `php5.6-apache` [(php5.6-apache/apache/Dockerfile)](https://github.com/bu-ist/php-test-runner/blob/master/php5.6-apache/apache/Dockerfile)

## Features

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

Run phpunit

```
$ docker run -v $(pwd):/var/www/html --rm bostonuniversity/php-test-runner
```

Get phpunit version

```
$ docker run -v $(pwd):/var/www/html --rm bostonuniversity/php-test-runner phpunit --version
```

Open shell

```
$ docker run -v $(pwd):/var/www/html --rm bostonuniversity/php-test-runner bash
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

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Notes:

- Xdebug is currently only configured to work when using Docker for Mac. We may fix this in the future. Feel free to submit a pull request if you want.
