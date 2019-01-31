# Docker

## Prerequisites
### Docker-Sync
Due to the poor performance of docker volumes on MacOSX docker ([GitHub issue 77: File access in mounted volumes extremely slow](https://github.com/docker/for-mac/issues/77)), these commands make use of [docker-sync](http://docker-sync.io/).  

#### Installation

Detailed installation instructions for docker-sync can be found at https://github.com/EugenMayer/docker-sync/wiki/1.-Installation but (assuming you have ruby installed) running `gem install docker-sync` should be all you need to do.

The in-built version of Ruby that ships with MacOSX appears to not install the docker-sync gem correctly.  Please install the latest version of Ruby via homebrew.

## Development Commands
**N.B. All commands MUST be run from the project root**

### Starting and stopping the dev environment 
#### Start the dev environment
```
dev/up [args]
```
Creates and launches new containers or restarts stopped containers.

The first time this command is run, it will take some time for `docker-sync` to synchronise the file system.

Any arguments accepted by `docker-compose up` will be valid for this command.

The first time you launch this, you'll probably want to run [composer install](#composer) and [assetic install](#symfony-console) as per the instructions further down.  

### Stop the dev environment 
```
dev/stop
``` 
Halts the running container and mounted volumes (equivalent to running `compose stop`).
```
dev/down
```
Shuts down and deletes all containers and `docker-sync` volumes (this won't delete anything on your host machine).
Equivalent to running `docker-compose down` 
 
### Executing commands
**N.B. All of these commands require a running container in order to execute.**
#### Symfony console
```
dev/console <cmd>
```
Executes `bin/console <cmd>` inside the `php-fpm` container.  Any arguments accepted by the Symfony console will be valid for this command.
#### Composer
```
dev/composer <cmd>
```
Executes `composer <cmd>` inside the `php-fpm` container.  Memory limits are set to unlimited.  Any arguments accepted by `composer` will be valid for this command.
#### Shell
```
 dev/ssh
``` 
Launches a shell inside the `php-fpm` container.
#### Arbitrary shell commands
```
dev/exec <cmd>
```
Executes `cmd` as an arbitrary shell command inside the `php-fpm` container.

#### Logs
```
dev/logs
```
Tails the logs from all containers.
 

### Docker Compose shortcuts
```
dev/docker-compose-dev
```
Runs `docker-compose` against the `<project root>/docker/docker-compose-dev.yml` file.  Running `dev/docker-compose-dev up` is equivalent to running `dev/up`.
 
### Navigating to the environment
The development environment can be navigated to at `http://localhost:8080`

The containerised NGinx server will also respond to the hostname of `http://worldanvil.local:8080` if you setup your hosts file to point that domain at `127.0.0.1`

## Jenkins
When `dev/up` is run, a [Jenkins](https://jenkins-ci.org) instance will be launched.  It can be reached on `http://localhost:18080`

All data for Jenkins job runs is stored under `<project root>/docker/data/jenkins`.

Jenkins will run the `World Anvil` pipeline against the latest version of the code in git. 

## Issues
 * In the event that port 8080 is already used by another process, you can change the port number in `/<project root>/docker/docker-compose.yml`
 * If an error is displayed, please make sure you are running the command from the project root - `dev/docker-compose.yml` and `dev/docker-sync.yml` both assume relative paths from the project root.

## TODO
 * Change the forwarded port to be obtained from environment variables if present 
