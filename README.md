# docker-php55
Ubuntu Trusty 64bit with PHP5.5 and Apache, comes with Zend Guard Loader and Zend OPCache

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
