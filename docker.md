---
title: Docker CLI
category: Devops
layout: 2017/sheet
---

Manage images
-------------

### `docker build`

```yml
docker build [options] .
  -t "app/container_name"    # name
  --build-arg APP_HOME=$APP_HOME    # Set build-time variables
```

### `docker container run`

```yml
docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
  # see `docker create` for options
```

Create an `image` from a Dockerfile.

#### Example

```
$ docker container run -it debian:buster /bin/bash
```
Run a command in an `image`.

Manage containers
-----------------

### `docker container create`

```yml
docker container create [OPTIONS] IMAGE [COMMAND] [ARG...]
  -a, --attach               # attach stdout/err
  -i, --interactive          # attach stdin (interactive)
  -t, --tty                  # pseudo-tty
      --name NAME            # name your image
  -p, --publish 5000:5000    # port map (host:container)
      --expose 5432          # expose a port to linked containers
  -P, --publish-all          # publish all ports
      --link container:alias # linking
  -v, --volume `pwd`:/app    # mount (absolute paths needed)
  -e, --env NAME=hello       # env vars
```

#### Example

```
$ docker container create --name app_redis_1 \
  --expose 6379 \
  redis:3.0.2
```

Create a `container` from an `image`.

### `docker exec`

```yml
docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]
  -d, --detach        # run in background
  -i, --interactive   # stdin
  -t, --tty           # interactive
```

#### Example

```
$ docker container exec app_web_1 tail logs/development.log
$ docker container exec -t -i app_web_1 rails c
```

Run commands in a running `container`.


### `docker container start`

```yml
docker container start [OPTIONS] CONTAINER [CONTAINER...]
  -a, --attach        # attach stdout/err
  -i, --interactive   # attach stdin

docker container stop [OPTIONS] CONTAINER [CONTAINER...]
```

Start/stop a `container`.


### `docker container ps`

```
$ docker container ps
$ docker container ps -a
$ docker container kill $ID
```
#### `Aliases`
ls, ps, list

Manage `container`s using ps/kill.


### `docker container logs`

```
$ docker container logs $ID
$ docker container logs $ID 2>&1 | less
$ docker container logs -f $ID # Follow log output
```

See what's being logged in an `container`.


Images
------

### `docker images`

```sh
$ docker images
  REPOSITORY   TAG        ID
  ubuntu       12.10      b750fe78269d
  me/myapp     latest     7b2431a8d968
```

```sh
$ docker images -a        # also show intermediate
$ docker images --quiet   # Only show image IDs
```

Manages `image`s.

### `docker rmi`

```yml
docker rmi b750fe78269d
```

Deletes `image`s.

## Clean up

### Clean all

```sh
docker system prune
```

Cleans up dangling images, containers, volumes, and networks (ie, not associated with a container)

```sh
docker system prune -a
```

Additionally remove any stopped containers and all unused images (not just dangling images)

### Containers

```sh
# Stop all running containers
docker container stop $(docker container ps -a -q)

# Delete stopped containers
docker container prune
```

### Images

```sh
docker image prune [-a]
```

Delete all the images

### Volumes

```sh
docker volume prune
```

Delete all the volumes

Also see
--------

 * [Getting Started](http://www.docker.io/gettingstarted/) _(docker.io)_
