# docker-php55

Custom Image for Oxid eShop with encrypted modules.

## Ingredients
Ubuntu Trusty 64bit with PHP5.5 and Apache, comes with Zend Guard Loader and Zend OPCache

## Configuration

There is some "custom config".

### Apache webserver
Custom vhost config for the apache webserver can be found in **apache_default**

### XDebug
Default XDebug configuration for phpstorm is in **xdebug_settings.ini** there are some directives which are "host-Specific" like **xdebug.remote_connect_back** and **xdebug.remote_host** can be overriden by Enviornment variables (see docker-compose example below).


## docker-compose example
Can be used in docker-compose.yml like this (Webserver mit code from ./src in the Document-Root listening on Host-Port 80)

    version: '2'
    services:
      hello-webserver:
        build: .
        volumes:
          - "./src:/var/www/html"
          - "/opt/typo3:/opt/typo3"
        ports:
          - 80:80
        tty: true
        logging:
          driver: json-file
          options:
            max-file: "5"
            max-size: "1m"
        environment:
          - REMOTE_CONNECT_BACK=1
          - REMOTE_HOST=192.168.33.1

This image is configured to work with XDEBUG in PHP-Storm. To get XDebug workig you will have to configure a pathmapping in PHP-Storm for the docroot/docker-Volume.
