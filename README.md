#**Finding Lane Lines on the Road** 
<img src="laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

**Step 1:** Getting setup with Python

To do this project, you will need Python 3 along with the numpy, matplotlib, and OpenCV libraries, as well as Jupyter Notebook installed. 

We recommend downloading and installing the Anaconda Python 3 distribution from Continuum Analytics because it comes prepackaged with many of the Python dependencies you will need for this and future projects, makes it easy to install OpenCV, and includes Jupyter Notebook.  Beyond that, it is one of the most common Python distributions used in data analytics and machine learning, so a great choice if you're getting started in the field.

Choose the appropriate Python 3 Anaconda install package for your operating system <A HREF="https://www.continuum.io/downloads" target="_blank">here</A>.   Download and install the package.

If you already have Anaconda for Python 2 installed, you can create a separate environment for Python 3 and all the appropriate dependencies with the following command:

`>  conda create --name=yourNewEnvironment python=3 anaconda`

`>  source activate yourNewEnvironment`

**Step 2:** Installing OpenCV

Once you have Anaconda installed, first double check you are in your Python 3 environment:

`>python`    
`Python 3.5.2 |Anaconda 4.1.1 (x86_64)| (default, Jul  2 2016, 17:52:12)`  
`[GCC 4.2.1 Compatible Apple LLVM 4.2 (clang-425.0.28)] on darwin`  
`Type "help", "copyright", "credits" or "license" for more information.`  
`>>>`   
(Ctrl-d to exit Python)

run the following commands at the terminal prompt to get OpenCV:

`> pip install pillow`  
`> conda install -c https://conda.anaconda.org/menpo opencv3`

then to test if OpenCV is installed correctly:

`> python`  
`>>> import cv2`  
`>>>`  
(Ctrl-d to exit Python)

**Step 3:** Installing moviepy  

We recommend the "moviepy" package for processing video in this project (though you're welcome to use other packages if you prefer).  

To install moviepy run:

`>pip install moviepy`  

and check that the install worked:

`>python`  
`>>>import moviepy`  
`>>>`  
(Ctrl-d to exit Python)

**Step 4:** Opening the code in a Jupyter Notebook

You will complete this project in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, run the following command at the terminal prompt (be sure you're in your Python 3 environment!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  
=======
# CarND Term1 Starter Kit (WIP, but works pretty well)

Software for Term 1 of the [Udacity Self-Driving Car Engineer Nanodegree](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013). Python 3 is used for entirety of term 1.

There are two ways to get up and running:

1. [Anaconda Environment](#anaconda)
2. [Docker](#docker)

## Anaconda

Install [miniconda](http://conda.pydata.org/miniconda.html) on your machine.

Next, setup the CarND term 1 environment.

To install:

```sh
git clone https://github.com/udacity/CarND-Term1-Starter-Kit.git
cd CarND-Term1-Starter-Kit
conda env create -f=environment.yml
```

To use:

```sh
# Enter the environment, should be called before you plan to work on a project (unless already active)
source activate carnd-term1
# Exit the environment
source deactivate
```

To cleanup downloaded libraries (remove tarballs, zip files, etc):

```sh
conda clean -tp
```

To uninstall the environment:

```sh
conda env remove -n carnd-term1
```

### Install Tensorflow for GPU

The current setup only installs the CPU version of TensorFlow. If you wish to use the GPU version follow the instructions [here](https://www.tensorflow.org/get_started).

## Docker

Using Docker to run your code consists of the following:

1. Install Docker on your computer
2. Pull the precompiled Docker image from Docker Hub
3. Run the image as a new container

You may also wish to run a [python module][doc/py_mod.md] or [ipython][doc/ipython.md].

### Install Docker On Your Computer

Instructions for installation very by operating system and version.

OS Specific instructions can be found below:

- Docker for Linux
   - [Linux](doc/docker_for_linux.md)
- Docker for Mac
   - [MacOS >= 10.10.3 (Yosemite)](doc/docker_for_mac.md)
- Docker Toolbox for Max
   - [MacOS >= 10.8 (Mountain Lion)](doc/docker_toolbox_for_mac.md)
- Docker for Windows
   - [Windows 10 Pro, Enterprise, or Education](doc/docker_for_windows.md)
- Docker Toolbox for Windows
   - [Windows 7, 8, 8.1, or 10 Home ](doc/docker_toolbox_for_windows.md)

**Recommended Shell:**

| OS                                       | Docker System               | Shell                      | Access Jupyter at |
|:-----------------------------------------|:----------------------------|:--------------------------:|:-----------------:|
| Linux                                    | Docker for Linux            | `bash`                     | `localhost:8888`  |
| MacOS >= 10.10.3 (Yosemite)              | Docker for Mac              | `bash`                     | `localhost:8888`  |
| MacOS >= 10.8 (Mountain Lion)            | Docker Toolbox for Max      | Docker Quickstart Terminal | `#DOCKERIP:8888`  |
| Windows 10 Pro, Enterprise, or Education | Docker for Windows          | `Windows PowerShell`       | `localhost:8888`  |
| Windows 7, 8, 8.1, or 10 Home            | Docker Toolbox for Windows  | Docker Quickstart Terminal | `#DOCKERIP:8888`  |

### Pull the Precompiled Docker Image from Docker Hub

A precompiled image with all dependencies required for the first term is
available on [Docker Hub][carnd_docker_hub].

Once you have docker working, pull the image using the following command:

```sh
docker pull udacity/carnd-term1-starter-kit
```

### Run The Image as a New Container

In your shell, navigate to the directory of a project, e.g.

```bash
$ cd ~/src/CarND-LaneLines-P1
```

From within this directory, you are going to run a Jupyter server. In order
to do this you must attach to the correct port and share a local volume.

The easiest way to share a local volume is via the `pwd` command, a shell
command that prints the working directory. This command will be used
differently based on your shell.

If you're using `Windows PowerShell`:

```sh
docker run -it --rm -p 8888:8888 -v ${pwd}:/src udacity/carnd-term1-starter-kit
```

If you're using `bash` or Docker Quickstart Terminal:

```sh
docker run -it --rm -p 8888:8888 -v `pwd`:/src udacity/carnd-term1-starter-kit
```

Let's break this down.

`docker run` is the command a startup and run a Docker container.

`-it` forces the container to run in the foreground (interactive mode) and
provides an I/O to the container.

`--rm` removes the container once it stops running.
It prevents the buildup of stale containers once you stop them from running.

`-p 8888:8888` maps port 8888 on our local machine to port 8888 in the Docker
container, this allows us to access port 8888 in the container
by visiting `localhost:8888`.

`-v ${pwd}:/src` mounts the pwd (present working directory) to the /src
directory in the container. Basically, this let's us access files
from our local machine on the docker container.

`udacity/carnd-term1-starer-kit` is the name of the container to run.

To learn more about Docker [visit the docs](https://docs.docker.com/engine/userguide/intro/).

### GPU support

The current image does not support GPU use. An image with GPU support is in the works although this would only work with a Linux base OS.

[carnd_docker_hub]: https://hub.docker.com/r/udacity/carnd-term1-starter-kit/
