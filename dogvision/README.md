# Docker container for running tensorflow in jupyter notebook with GPU support. 
## Notable included libraries: 
* numpy
* pandas
* matplotlib
* scikit-learn
* tensorflow
* tensorflow-hub

## Instructions for running custom tensorflow-gpu-jupyter container
This repository contains a file called "dockerfile". This file is basically a script for setting up the docker container. Use the following commands to build the container and run it.
1. Run `docker build -t <DIRNAME> .` to build the container.
2. Run `docker run --gpus all -it -v $PWD:/<DIRNAME> -w /<DIRNAME> -p 8888:8888 -p 6006:6006 <DIRNAME>` to run the container.

The above run command runs the docker container mapped to your current working directory. Any changes made to files within the container will be reflected in the working directory as well. 

When the run command is ran, it will give you the URL to the jupyter kernel to use with the associated security token. You can then run your jupyter notebook like normal.

## Running default tensorflow-gpu container
To run the default tensorflow container with gpu support for temporary use (all files added to the container will be deleted when the container is stopped). Run `docker run --gpus all -it tensorflow/tensorflow:latest-gpu bash`. Use the same -v attribute shown in the above docker run command to map it to your working directory.

## Recommendations
1. Use vscode extension to streamline the start and stopping of containers.
2. Create a new directory and map the container(you can always delete if needed).
3. Use jupyter notebook. 
