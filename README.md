## Redis Debug Build Docker Image ##
[![Build Status](https://travis-ci.org/y-asaba/docker-redis-debug.svg?branch=master)](https://travis-ci.org/y-asaba/docker-redis-debug)

This Dockerfile builds Redis server with debugging information.

**Please do not use this image in production envrionment because redis-server is compiled without optimization (-O0 option).**

### How to Build ###

#### Redis 4.0 ####

```
$ docker build -t redis-debug-4.0 4.0
```

#### Optional

Setting the target Version

```
$ docker build --build-arg REDIS_VERSION=4.0.11 -t redis-debug-4.0 4.0
```

### How To Run the docker image ###

#### Docker run ####

```
$ docker run  -p 6379:6379 -t --cap-add=SYS_PTRACE --security-opt seccomp=unconfined redis-debug-4.0 -it /bin/bash
>  cd /root/redis-4.0.11/src
> gdb ./redis-server
gdb> r --protected-mode no

```
