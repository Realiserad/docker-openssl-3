# About

Minimal docker image with [OpenSSL 3.0](https://www.openssl.org/blog/blog/2021/09/07/OpenSSL3.Final).

# Why

Useful for testing OpenSSL commands when you need to be at the forefront, without having to touch your own system, potentially wreaking havoc in the process. 

Personally I had to run OpenSSL to try out the new CMP client, but I wanted to do so without messing around with the existing (older) OpenSSL on my Ubuntu machine.

Can also be used a a base layer, e.g. when building a container for your webserver or another application depending on OpenSSL.

# Build and Run

Build the container. Compiling OpenSSL is slow, this takes about 10 minutes on my machine, so be prepared with a cup of coffee.

```
docker build -t realiserad/openssl:3.0.0 .
```

Run the container and open a shell.
```
docker run -it realiserad/openssl:3.0.0
```

Now you can test your new shiny OpenSSL installation:
```
> openssl version
OpenSSL 3.0.0 7 sep 2021 (Library: OpenSSL 3.0.0 7 sep 2021)
```

Pull From DockerHub
===================

You can also pull a [pre-built image directly from DockerHub](https://hub.docker.com/repository/docker/realiserad/openssl3).
```
docker pull realiserad/openssl3
```

Use With Docker Compose
=======================

To use this container with Docker Compose, use the following ``docker-compose.yml``:
```
version: '3'
networks:
  router:
    driver: bridge
services:
  openssl:
    container_name: openssl
    image: realiserad/openssl3
    networks:
      - router
    stdin_open: true
```

Start the container with ``docker-compose up``.

To access OpenSSL inside the container, open a shell with ``docker exec -it $(docker ps | grep realiserad/openssl | awk '{ print $1 }') /bin/sh``.
