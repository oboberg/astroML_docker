astroMLdock
=============

[![Docker Automated build](https://img.shields.io/docker/automated/oboberg/astroml.svg)](https://hub.docker.com/r/oboberg/astroml/)

A Docker image with everything you need to run the [astroML](http://www.astroml.org/) python module. astroML was written by [Vanderplas et al, proc. of CIDU, pp. 47-54,
2012](http://ieeexplore.ieee.org/document/6382200/?tp=&arnumber=6382200).

# Introduction

astroML is python module with many of the tools
one needs to apply machine learning and data mining techniques to astronomical
datasets and questions.

The [astroML](http://www.astroml.org/) module was developed to accompany the textbook
[*Statistics, Data Mining, and Machine Learning in Astronomy*](http://www.astroml.org/index.html#textbook)
and provides all of the code needed to reproduce the figures in the textbook. Recreating
these figures is a good way to learn how to use astroML and how to use jupyter
notebooks through Docker.

## What's in the Docker image

The base of this Docker image is the [jupyter datascience notebook](https://hub.docker.com/r/jupyter/datascience-notebook/).
This provides pandas, matplotlib, scipy, seaborn, scikit-learn, scikit-image,
sympy, cython, patsy, statsmodel, cloudpickle, dill, numba, bokeh, and a number of other useful packages.
On top of this software we also install astropy, pyMC, healpy, astroML, astroML_addons,
and LaTex, giving you the complete environment needed to run the astroML plotting
examples right out of the box.

## Making the textbook figures

This section will walk through exactly how to run a Docker container that will
allow you to create the textbook figures through a jupyter botebook.

1. Clone the github repository with the source code for the figures on to your
local machine and change into that directory.
~~~
git clone https://github.com/astroML/astroML_figures
cd astroML_figures
~~~

2. Run a Docker container based of the Docker iamge `oboberg/astroml`. Make
sure you are running this command from the `astroML_figures` directory you just
downloaded.
~~~
docker run -it --rm \
       -p 8888:8888 \
       -v $PWD:/home/jovyan/work \
       oboberg/astroml
~~~
The docker image will be automatically pulled from the Docker Hub if you do not
already have it locally.

3. After running the command in step `2` you will see the familiar jupyter notebook
dialog and will be asked to copy and paste a URL into your local browser. Here
is an example, not a command. Make sure you do not have any thing else running on
port 8888.
~~~
Copy/paste this URL into your browser when you connect for the first time,
to login with a token:
    http://localhost:8888/?token=sometoken
~~~
Copy and paste the URL you are given into a browser on your local machine and you
will see the jupyter notebook home page.

4. Create a new jupyter notebook by clicking the `New` dropdown menu in the upper
right hand corner and then select `Python3`. This should atomically open
a new notebook called `Untitled` in a new browser tab.

5. In a blank cell try running the following command, included the `%`.
~~~
In [1]: %run book_figures/chapter1/fig_moving_objects_multicolor.py
~~~
If the figure does not show up run the cell a second time. You can see this
uses the jupyter magic command `%run`. This because the script to create the
plot is a plain python script, not a jupyter notebook.

6. To actually see and modify the code we can use the jupyter magic command
`%load`, which will populate a notebook cell with the contents of a python
script.
~~~
In [2]: %load book_figures/chapter1/fig_moving_objects_multicolor.py
~~~
This command only populates the cell so it will still need to be executed with
a `shift+enter`.

7. You can now create what ever figures you would like from the book, or make up
your own. Any of the new jupyter notebooks you create will be saved to your
local directory because it was mounted in the container during the run command
in step `2`. The option `-v $PWD:/home/jovyan/work` mounts the `$PWD` of your
local machine (in this example `astroML_figures` ) inside the container as
`/home/jovyan/work`.







## Building the image yourself

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
