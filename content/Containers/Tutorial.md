---
title: "Getting Started"
date: 2018-10-25T10:30:22+01:00
draft: False
---

1) Make an account on the website [hub.docker.com](https://hub.docker.com)

Make the username something sensible as we'll have to use it soon!

2) If you haven't already, try "docker run ubuntu:18.04". This downloads an image containing Ubuntu 18.04.

3) Now, we'll create a file called "Dockerfile" in a single folder. The Dockerfile is a configuration script for building an image.

* Create a directory by doing:

> mkdir docker-tutorial

* Change directory into the folder:

> cd docker-tutorial

4) First line: 'from ubuntu:18.04'

5) Now, we can start installing things inside the image.

6) First do "RUN apt-get update" - note all commands have 'RUN' at the beginning.

7) Then "RUN apt-get install -y python3"

Now, you have an image which:
* Is based on Ubuntu 18.04. You could change this to another Linux distribution if you wanted, such as CentOS.
* Contains Python 3.

This is the general principle of containers - you build them up in steps until they have everything you need to run real applications.

8) Now let's build the image try building the container from the script file with:

docker build . -t YOURUSERNAME/myimage

Breaking this down:
* Docker is the application.
* We're running Docker's build command
* "." refers to the file location - it's saying "build the Dockerfile in this folder"
* -t YOURUSERNAME/myimage - if you're not familiar with Linux, adding a dash is a common way of signalling how to pass information to a command.
  "-t" just means build the image with the tag YOURUSERNAME/myimage

Every time you add another command to the script, you create a new *layer*.

A layer is the essentially just a list of differences between the previous command and the present one.

Your container image is built up of multiple layers. If you want to add a new command,
you don't have to rebuild completely from scratch - Docker is clever enough to start from the *last common layer*. These layers take up storage space, however.

That means though, if you change the programmes installed with apt-get on the second line of the script, all subsequent steps must be repeated, because Docker can't work out if subsequent steps are independent or not of each other.

9) Now we've installed Python in the image, how do we use the image's version of Python?

We can do this in two ways - similar but different!

1) Start a container from the image interactively, and launch the programme:

To run interactively, must add the "-i" flag

> docker run -i -t YOURUSERNAME/myimage

2) Create a container:

> docker create --name mytest YOURUSERNAME/myimage
> docker start --name mytest
 



10) We can save the docker container to a file with

docker save YOURUSERNAME/mycontainer > myimage.tar

You can compress the image if you want:

gzip -f myimage.tar

You can load it again with 

docker load myimage.tar.gz


11) However, not normally necessary - much easier just to use Docker Hub. Free uploads of containers if public, one private container per account.

Make a repository called 'mycontainer' on your Dockerhub account

12) docker login - put in username and password

13) docker push YOURUSERNAME/mycontainer

14) Your container is now online!

15) Just to show how you can pull them, let's now delete the containers.

Lots of commands for deleting stuff... Bit confusing!

# docker system prune

Deletes everything that are not associated with a container - "dangling". Add the "-a" flag to remove additionally stopped containers and all unused images.

Removing a specific image

docker images gives list of all images you've created, including intermediate layers.

Copy the image id of the image you want to remove 

> docker rmi IMAGEID

May need to do:

> docker rmi IMAGEID -f

If other images depend on it - they will also be deleted!

Remove all images:

> docker images -a
> docker rmi $(docker images -a -q)

16) Now pull the image we uploaded:

> docker pull YOURUSERNAME/dependencies





