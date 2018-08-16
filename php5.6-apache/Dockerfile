FROM php:5.6-apache

# install the PHP extensions we need
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libjpeg-dev \
		libpng-dev \
        git \
        subversion \
        mysql-client \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install gd mysqli opcache
# TODO consider removing the *-dev deps and only keeping the necessary lib* packages

# set recommended PHP.ini settings
# see https://secure.php.net/manual/en/opcache.installation.php
RUN { \
		echo 'opcache.memory_consumption=128'; \
		echo 'opcache.interned_strings_buffer=8'; \
		echo 'opcache.max_accelerated_files=4000'; \
		echo 'opcache.revalidate_freq=2'; \
		echo 'opcache.fast_shutdown=1'; \
		echo 'opcache.enable_cli=1'; \
	} > /usr/local/etc/php/conf.d/opcache-recommended.ini

RUN a2enmod rewrite expires

# Install phpunit
WORKDIR /tmp
RUN docker-php-ext-install pcntl
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php composer-setup.php --install-dir=/usr/bin --filename=composer \
    && php -r "unlink('composer-setup.php');" \
    && composer require "phpunit/phpunit:~5.7" --prefer-source --no-interaction \
    && composer require "phpunit/php-invoker" --prefer-source --no-interaction \
    && ln -s /tmp/vendor/bin/phpunit /usr/local/bin/phpunit \
    && sed -i 's/nn and/nn, Julien Breux (Docker) and/g' /tmp/vendor/phpunit/phpunit/src/Runner/Version.php;
WORKDIR /var/www/html

# Install xdebug
RUN pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && rm -rf /tmp/pear/
# Configure xdebug
RUN { \
      echo ''; \
      echo 'xdebug.remote_enable=1'; \
      echo 'xdebug.remote_autostart=1'; \
      echo 'xdebug.remote_host="docker.for.mac.localhost"'; \
      echo 'xdebug.remote_port="9000"'; \
      echo 'xdebug.remote_log="/var/log/xdebug.log"'; \
    } >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini