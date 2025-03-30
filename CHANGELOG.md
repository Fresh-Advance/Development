# Change Log for Sieg Development base

All notable changes to this project will be documented in this file.
The format is based on [Keep a Changelog](http://keepachangelog.com/)
and this project adheres to [Semantic Versioning](http://semver.org/).

## [v4.3.0] - Unreleased

### Added
- SSL is enabled and preconfigured by default (import the `containers/httpd/certs/fresh_advance_localhost_ca.crt` authority to your browser to trust the certificates)

## [v4.2.0] - 2025-02-19

### Added
- PHP 8.3 and 8.4 supported

### Changed
- Use 8.3 as default PHP version

### Fixed
- Remove obsolete "version" option from docker-compose.yml.dist file

## [v4.1.0] - 2024-03-27

### Added
- `MYSQL_VERSION` environment variable to .env file
- PHP images regenerated weekly to use the latest updated official php-fpm bases

### Changed
- Default mysql container version is changed from 5.7-debian -> 8.0-debian, and its configurable in .env file

### Fixed
- Recipes converted to docker compose v2, as this part was still using the first version

## [v4.0.0] - 2023-10-09

### Added
- Create "example" database in mysql container by default
- Wait for services healthy during `make up`
- New recipe - "phpunit" allows fast start with preconfigured phpunit

### Changed
- Switch to docker compose v2

### Fixed
- Improve `make reset` to remove "source" directory, as its used in all examples

## [v3.2.0] - 2023-08-25

### Added
- PHP 8.2 supported

### Changed
- Do not cache local .user.ini values
- Default PHP version is changed from 8.0 -> 8.1

## [v3.1.0] - 2022-08-07

### Added
- Expose mysql port for local client access
- Github is trusted by default
- New command: ``make reset`` - removes all configuration files created by ``make setup``

### Changed
- Images regenerated with one name but separate versions which fits the php version

### Fixed
- .env file php version default value fixed
- Improve client host calculation to work by default on Windows and Mac systems
- Use debian based mysql containers, as new ones goes with different configurations, most likely something will not fit, needs further improvements.

## [v3.0.0] - 2022-02-04

### Added
- PHP_VERSION as environment variable
- Example recipe to install example scripts :) The idea is to create multiple different recipes in the future
- Possibility to build specific docker-compose.yml file with console command!
  - The file can be build by merging separate smaller chunks (services) together
  - The ``make addservice`` command introduced. Example of usage: ``make file=services/apache.yml addservice``

### Changed
- Example files moved to `recipes/default/examples` directory
  - Files will be copied during the example recipe - ``make example``.
- Default docker-compose.yml.dist have been split to multiple service files and moved to services directory
  - Now, no services are installed by default anymore, but rather, use the ``make addservice`` to add specific services
  - To add all basic services (php, mysql and apache), the ``make addbasicservices`` command can be used

### Fixed
- Readme adjusted by latest changes, please, read from the start, again.

## [v2.0.0] - 2021-12-12

### Added
- PHP 8.0 and PHP 8.1 containers!
- Register a link to apache container for the php container (so its possible to ping one by url)

### Changed
- Base container repositories renamed to siegfuse/php-fpm-X.X-base where (X.X is php version)
- ``latest`` tag of base container is used by default
- Move SPX package installation to base php container. 
  - 7.4 base container rebuilt with latest dependencies and spx.
  - It will allow faster start of the environment.
- ``containers/php-fpm/user.ini`` is renamed to custom.ini.dist. Setup copies it to custom.ini 

### Fixed
- Fix wrong rights for ~/.composer directory. Now composer commands will work properly.

## [v1.4.0] - 2021-11-20

### Added
- Copy ``containers/httpd/project.conf.dist`` to ``containers/httpd/project.conf`` during ``make setup``
- Copy ``docker-compose.yml.dist`` to ``docker-compose.yml`` during ``make setup``

### Changed
- Rename project.conf to project.conf.dist
- Updated the php-fpm image, so it have:
  - composer version 2
  - xDebug 3
- Use node latest

### Fixed
- Configure remote debugging on xDebug 3
- Fix wrong rights on volume synced directory in home of php container
- Update default server for adminer
- Remove node container after use

## [v1.3.0] - 2021-06-04

### Added
- Preconfigure SPX - simple php profiler

### Changed
- Mysql data is now saved between session. Mysql databases are synced to the host system in `data/mysql` directory

## [v1.2.0] - 2021-03-18

### Added
- Mailhog container preconfigured in docker-compose
- Example with php sending email added
- Makefile command ``make php`` to access bash on php container

### Changed
- Reconfigured php log and profiler paths to be always available and no additional configuration required. Available in `data/php` directory.

## [v1.1.0] - 2021-03-16

### Added
- Makefile with main commands:
    - preconfigure with ``make setup``
    - start containers with ``make up``
    - stop containers with ``make down``

## [v1.0.0] - 2019-10-23

[v4.3.0]: https://github.com/Sieg/development/compare/v4.2.0...v4.3.0
[v4.2.0]: https://github.com/Sieg/development/compare/v4.1.0...v4.2.0
[v4.1.0]: https://github.com/Sieg/development/compare/v4.0.0...v4.1.0
[v4.0.0]: https://github.com/Sieg/development/compare/v3.2.0...v4.0.0
[v3.2.0]: https://github.com/Sieg/development/compare/v3.1.0...v3.2.0
[v3.1.0]: https://github.com/Sieg/development/compare/v3.0.0...v3.1.0
[v3.0.0]: https://github.com/Sieg/development/compare/v2.0.0...v3.0.0
[v2.0.0]: https://github.com/Sieg/development/compare/v1.4.0...v2.0.0
[v1.4.0]: https://github.com/Sieg/development/compare/v1.3.0...v1.4.0
[v1.3.0]: https://github.com/Sieg/development/compare/v1.2.0...v1.3.0
[v1.2.0]: https://github.com/Sieg/development/compare/v1.1.0...v1.2.0
[v1.1.0]: https://github.com/Sieg/development/compare/v1.0.0...v1.1.0
[v1.0.0]: https://github.com/Sieg/development/compare/020f452b2a...v1.0.0
