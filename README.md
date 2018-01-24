astroMLdock
=============

[![Docker Automated buil](https://img.shields.io/docker/automated/oboberg/astroml.svg)](https://hub.docker.com/r/oboberg/astroml/)

A Docker image with everything you need to run the [astroML](http://www.astroml.org/) software.

To build the Docker image yourself do the following after cloning this repository.

```
$ docker build -t "astroml" .
```

When the Docker image is finished building, run the following command to start
a docker container and a jupyter notebook. Note that the `$PWD` where this
command is run will mounted inside the docker container.

```
$ docker run -it --rm \
       -p 8888:8888 \
       -v $PWD:/home/jovyan/work \
       astroml
```

If you do not want to build your own image you can also pull an image from
Docker Hub and run the container with the following command:

```
$ docker run -it --rm \
       -p 8888:8888 \
       -v $PWD:/home/jovyan/work \
       oboberg/astroml
```
