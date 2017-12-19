# wp-phpunit-xdebug
Docker image that has composer, phpunit and xdebug installed and configured to be used when testing WordPress themes and plugins with this unit test setup https://github.com/wp-cli/sample-plugin.

This image does not actually come with any WordPress files since the script in the above mentioned repository downloads and installs WordPress.

Note: Xdebug is currently only configured to work when using Docker for Mac. I am looking to get it working on any host machine.
