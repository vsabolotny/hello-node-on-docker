# Hello node on docker

A demo version for test purposes. 

Corresponding repository on the dockerhub is https://hub.docker.com/repository/docker/vsabolotny/hello-node-on-docker.

## How to run it on ARM64v8

Official documentation https://docs.docker.com/docker-for-mac/multi-arch/.

### Most important steps

Create a new builder:
```
$ docker buildx create --name mybuilder
mybuilder
```

Start to use and to inspect the options:
```
$ docker buildx use mybuilder
$ docker buildx inspect --bootstrap
```

Check the existing builder:
```
$ docker buildx ls
NAME/NODE    DRIVER/ENDPOINT             STATUS  PLATFORMS
mybuilder *  docker-container
  mybuilder0 unix:///var/run/docker.sock stopped
default      docker
  default    default                     running linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
```

Build a couple of image variants, and push them to Docker Hub:
```
$ docker buildx build --platform linux/amd64,linux/arm64v8 -t vsabolotny/hello-node-on-docker --push .
```

Inspect the image:
```
$ docker buildx imagetools inspect vsabolotny/hello-node-on-docker
```