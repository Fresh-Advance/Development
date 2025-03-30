# Development base

Docker based local development environment. Php and Npm users are synced with the current user, 
so we will have all the rights to modify and access the content generated by using container commands.

## What we have here

For the start:

* Apache 2.4 (based on original httpd:2.4-alpine container)
  * SSL is enabled and preconfigured by default (import the `containers/httpd/certs/fresh_advance_localhost_ca.crt` authority to your browser to trust the certificates)
  * HTTP/2 is enabled by default
* PHP 7.4 / 8.0 / 8.1 / 8.2 / 8.3 / 8.4 fpm (based on original php:x.x-fpm containers) with:
  * composer 2
  * xDebug 3 with remote debug and profiler preconfigured
  * error reporting enabled
* MySQL 5.7(any other version can be easily used) with adminer (original mysql container used)
* Mailhog preconfigured to catch outgoing emails
* SPX preconfigured (PHP Simple Profiler - https://github.com/NoiseByNorthwest/php-spx)
* Npm container preconfigured, so you can easily regenerate grunt/gulp/other builder assets for modules/themes easier (based on node:latest)
* Chrome based selenium service available, for running your selenium tests (based on selenium/standalone-chrome-debug)

## Requirements

* Docker (https://docs.docker.com/get-docker/)
* Docker compose (https://docs.docker.com/compose/install/)
* ``127.0.0.1 localhost.local`` - in your ``/etc/hosts`` file

* (Optional) Import the `containers/httpd/certs/fresh_advance_localhost_ca.crt` authority to your browser to trust the certificates

## Quick start

#### 1. Prepare the project directory

Run this command to Create a directory (currently `myProjectName`) and clone this development base:
```
echo myProjectName && git clone https://github.com/Sieg/development.git $_ && cd $_
```

#### 2. Environment example

Run example script which prepares several example files for you to see this environment functionality
```
./recipes/default/example/run.sh
```

#### 3. Brief description whats available now:

Access the website through the http://localhost.local
* phpinfo shown on index page
* example with database connection
* example with email sending and catching it with mailhog
    * run the composer install on php container first.

Adminer is available via http://localhost.local:8080
* Server: mysql
* Credentials: root/root

Mailhog is available via http://localhost.local:8025/

SPX preconfigured and UI accessible via http://localhost.local?SPX_KEY=dev&SPX_UI_URI=/

## Longer start

This example shows more precise configuration which can be used for your project. It is real usage flow:

```
# clone the development environment to myProjectName directory
echo myProjectName && git clone https://github.com/Sieg/development.git $_ && cd $_

# setup rights and basic configuration files
make setup

# add php, mysql and apache services (they are grouped in one command, but can be added separately if needed)
make addbasicservices

# add selenium container to the docker-compose
make file=services/selenium-chrome.yml addservice

# ensure you have source directory available, as its configured as webroot by default
mkdir source

# start everything
make up

.... Now everything is up and ready for work ....

# stop everything when its enough :)
make down
```

## Running php stuff

We can connect to the php container and do the stuff in there:
```
make php
php -v
```

Note: ``make php`` is just an alias for ``docker-compose exec php bash``

We can call commands directly without connecting to the container:
```
docker-compose run php php -v
```

## Running npm commands

### Direct call
```
docker-compose run node npm install bootstrap
```

### Connect to node container
```
make node
```

## Configurations

### Apache

Custom configuration file: ``containers/httpd/project.conf``.

### PHP

Select PHP version to be used in docker-compose php container configuration.
Custom configuration file for php settings: ``containers/php-fpm/custom.ini``.

### Remote debugging with PHPSTORM

* Configure the CLI Interpreter
* Create a Server configuration and set mapping as source:/var/www/ 

## Recipes

Recipes directory contains very simple scripts that can be used for fast start 
of certain preconfigured environments:

* `default/example` - is installing basic environment example that is described in "Quick start" section
* `default/phpunit` - is a preinstalled PHPUnit installation, so TDD kata's can be practiced
  * The `docker-compose exec php composer tests-coverage` command, runs tests. 
  * Also `make php` and then `composer tests-coverage` or `composer tests-unit` can be used

## Inspired by OXID, but also used by OXID! :)
* https://github.com/OXID-eSales/oxvm_base
* https://github.com/OXID-eSales/oxvm_eshop
* https://github.com/OXID-eSales/docker-eshop-sdk

## Contributing

You like to contribute? 🙌 AWESOME 🙌 Throw a pull request, with the description why you/we need it and instructions how to test it out :)
