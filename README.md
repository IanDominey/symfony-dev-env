# Docker based Symfony development environment and scripts

Optimised for development on OSX using docker-sync.

Using it requires installation of [docker-sync](http://docker-sync.io/ ).

Use this repo as a template in which to run a Symfony application.

## Commands

* `dev/docker-up` launches the environment (accepts all switches accepted by `docker-compose up`)
* `dev/docker-down` shuts down the environment
* `dev/docker-ssh` launches a shell inside the php-fpm container
* `dev/docker-logs` views `docker-compose` logs
* `docker-npm` launches `npm` inside the php-fpm container
* `docker-console` launches the Symfony console inside the php-fpm (accepts all symfony console commands)
* `docker-composer` launches composer inside the php-fpm container