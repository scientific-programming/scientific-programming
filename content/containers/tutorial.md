---
title: "Getting Started with Docker"
date: 2018-10-26T09:41:56+01:00
draft: false
weight: 30
---

### First Steps
1) Make an account on the website https://hub.docker.com

Make the username something sensible as we'll have to use it soon!

1) If you haven't already, try "docker run ubuntu:18.04". This downloads an image containing Ubuntu 18.04.

2) Now, we'll create a file called "Dockerfile" in a single folder. The Dockerfile is a configuration script for building an image.

* Create a directory by doing:

```bash
mkdir docker-tutorial
```

* Change directory into the folder:

```bash
cd docker-tutorial
```
3) Create a file called Dockerfile in this directory, and put as the first line:

```Dockerfile
from ubuntu:18.04'
```

4) Now, we can start installing things inside the image. We do this by adding lines to the Dockerfile; a command to run is prefaced by "RUN". If you're not familiar with Linux, and are primarily a Windows or Mac user, it may seem a little odd to install programmes using typed out commands, but it can be very powerful. For Ubuntu, there are basically two commands you need to know.

First, we'll update the list of Ubuntu packages which can be installed; note that this is almost always necessary. To do this, add:

```Dockerfile
RUN apt-get update
```

to the file.

6) Once this is completed, you can then choose to install programmes. We're going to use Python for this example, but you can pick any programmes you like for your own Docker containers. Here, we just add the line:

```Dockerfile
RUN apt-get install -y python3
```

which tells Ubuntu to install Python 3 in the container. The "-y" flag here just tells apt-get, the programme used in Ubuntu for installing programmes, not to prompt for confirmation.

Now, you have a script which tells Docker to build a container which:
* Is based on Ubuntu 18.04. You could change this to another Linux distribution if you wanted, such as CentOS.
* Contains Python 3.

This is the general principle of containers - you build them up in steps until they have everything you need to run real applications.

Now, we can tell Docker to run a command when the container is launched. We do this using a slightly different syntax:

```
CMD /bin/bash
```

This just tells Docker to launch the Bash shell. From this, we can launch all of the programmes installed into the container. Alternatively, we could just as easily write:

```
CMD /

7) Now let's actually build the container image from the script file. We do this using the following command - replace "YOURUSERNAME" with your username for the account we created with Dockerhub earlier.

```Bash
docker build . -t YOURUSERNAME/myimage
```

Breaking this command down:

* Docker is the application.

* We're running Docker's build command

* "." refers to the file location - it's saying "build the Dockerfile in this folder"

* -t YOURUSERNAME/myimage - if you're not familiar with Linux, adding a dash is a common way of signalling how to pass information to a command. Here, "-t" just means build the image with the tag YOURUSERNAME/myimage

### More concepts

Every time you add another command to the script, you create a new *layer*.
A layer is the essentially just a list of differences between the previous command and the present one. Your container image is built up of multiple layers. If you want to add a new command, you don't have to rebuild completely from scratch - Docker is clever enough to start from the *last common layer*. These layers do take up storage space, however.

That means though, if you change the programmes installed with apt-get on the second line of the script, all subsequent steps must be repeated, because Docker can't work out if subsequent steps are independent or not of each other.

7) Now we've installed python3 in the image, how do we use it?

We can do this in two ways - similar but quite different!

1) Start a container from the image interactively, and launch the programme:

To run interactively, we must add the "-i" flag. If we don't do this, the programme will launch, but will freeze!

```bash
docker run -i -t YOURUSERNAME/myimage
```

Then, just run
```
python3
```
to launch the Python interpreter.

2)
* Create a container from the image, and give it the name 'mytest'
```bash
docker create --name mytest YOURUSERNAME/myimage
```
* Then, start the container:

```bash
docker start --name mytest
```
*


### Saving the Container

1) We can save the docker container to a file with

```bash
docker save YOURUSERNAME/mycontainer > myimage.tar
```

You can compress the image if you want with the command

```bash
gzip -f myimage.tar
```
You can load it again with

```bash
docker load myimage.tar.gz
```

2) However, it's not normally necessary to save containers like this - much easier just to use Docker Hub. Free uploads of containers if public, one private container per account.

Make a repository called 'mycontainer' on your Dockerhub account

3) Now, on your computer, run the command:
```
docker login
```
You will be prompted for your username and password for Dockerhub. Enter them.

11) Now, we can publish the container online using:

```bash
docker push YOURUSERNAME/mycontainer
```

12) Your container should now be available online. That means, someone else can download it using the 'docker pull' command, and run the same programmes as you in the same way.

13) Just to prove it to you, let's now delete the containers.

There are lots of commands for deleting containers and images - this is quite confusing!


If you want to remove *everything*, you can run:
```bash
docker system prune
```
Deletes everything that are not associated with a running container - "dangling". Add the "-a" flag to remove additionally any stopped containers and all unused images.


If you just want to remove a specific image, you can run

```Bash
docker images
```

This gives a list of all images you've created, including intermediate layers.
Copy the image id (the long string of numbers) of the image you want to remove:

```bash
docker rmi IMAGEID
```
You may need to add the flag '-f' if you get an error here:

```
docker rmi IMAGEID -f
```
Note: if other images depend on the image you are deleting, they will also be deleted!

Remove all images:

```bash
docker images -a
docker rmi $(docker images -a -q)
```

14) Now pull the image we uploaded:

```
docker pull YOURUSERNAME/dependencies
```


### Further steps

TBD: Check Windows mount path syntax

Often, we want to install programmes in the container in order to manage dependencies, but we need to have them act on files stored on the computer itself. This can easily be achieved by mounting folders into the container, so that they are visible inside it.



TBD: Mounting Ports: Explain what ports are? Networking end points - send messags between? Is this sufficient? TCP vs UDB - Docker uses TCP by default. Not sure this is relevant to mention.
