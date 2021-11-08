# Docker

Docker is the tool that we are going to use to create and manage containers ,which are independent environments . Some of the main functions and a little set up tutorial will be showed in this document.



## Set up tutorial 

* First you need to download and install docker (distribution dependent)

* Then we need to enable and activate the service:

  ` $systemctl enable docker ` 

  `$systemctl start docker`  

Now the service is active, and we can start using it.

## Docker images

To make a good pizza, we need a good base. Same with Docker and its images. A docker image is the local "SO" over which applications will be running. If we want to use an image to create a container. 



## Docker first steps

The first step is to pull an image: 

`$docker pull <name> `

Where name can be  any distribution, let's take ubuntu in this example. We run the command and download the image. Then, we create the container by typing:

`$ docker run -d -t --name my_container ubuntu `

There, -d means that the container will run in the background (else the container will inmediatly stop after being created) and -t is used to allocate a pseudo-TTY 

Then, if we want to start a terminal in the container, we just have to type: 

`docker exec -it my_container bash  `



## Dockerfiles

Dockerfiles allow us to create custom images. For example, if we want to run a web appplication, we might aswell have nginx or Apache already installed in our image. 

In order to do that, there is a very good tutorial here: https://linuxconfig.org/how-to-build-a-docker-image-using-a-dockerfile

## Our project

Here, we will add the documentation for the build of our own project [TO DO].





Also refer to the docker complete documentation: https://docs.docker.com/  

  

