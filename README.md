astroMLdock
=============

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
