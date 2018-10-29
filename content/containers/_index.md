---
author:
- Ryan Pepper
date: October 29th 2018
title: 'Containers'
draft: false
weight: 20
---

### What are containers?

Containers provide a mechanism for setting up an environment with many software dependencies. They can be simple, with a limited number of simple programmes installed, or can be used to set up complex software. In addition, they allow software from different operating systems to be used natively; an Ubuntu package could be used on a RHEL Linux system without any issues.

Users write scripts in a simple standardised way, and this is primarily bundled with the project, and passed on to other developers in order to give them the same environment to work from when developing software. A built container can also be hosted online freely, which is useful when building the dependencies takes a long time.

These features might seem familiar if you've come across Virtual Machines in the past. The primary advantage of containers is that they do not incur the performance penalty that virtual machines do, if they are run on a Linux operating system (in general).

### What are containers not?

Containers are not always a great way to *distribute* scientific software to people who are going to use it, particularly when the code is compiled. This is because hardware variances mean that software has generally got to be compiled for the oldest possible machine it could be used for. This means that for optimal performance, multiple versions of the same container need to be compiled. This is particularly important when running high performance software which runs on supercomputers.

Because of this, making your code run in a container is not 'enough' to distribute software; it is still necessary to make a comprehensive list of the dependencies necessary to run the software, with versions. However, it takes the pain out of having multiple developers working in different environments which what may prove to be incompatible versions of dependencies. It also should not be used as a way of avoiding updating scientific software because it now runs everywhere.

{{% panel theme="info" header="Terminology" %}}
* Host - A physical computer running VM/container.
* Container - An operating system level virtualised environment in which software is installed.
* Image - A container which has been saved to a file.
* Hypervisor - The software which runs a virtual machine.
* Kernel - Core OS components and functions.
{{% /panel %}}

###  Comparisons with Virtual Machines
As mentioned before, despite not being virtual machines, containers act like them in many ways.

####  How are containers like VMs?
* *Isolated environment* - Processes run isolated from other processes -
they can’t access hardware resources they aren’t allocated.
* *They are independent* - Generally you can be given a container image or
a virtual machine image and use that to run a piece of software without
doing anything else.

### How are containers not like VMs?
* *They use Kernel features of the host* - Linux supports process and
resource partitioning and isolation (cgroups, OverlayFS, kernel
namespacing), which allows containers to use a subset of resources. If you're really
interested in the underlying mechanism by which Docker works, have a look [here](https://docs.google.com/presentation/d/10vFQfEUvpf7qYyksNqiy-bAxcy-bvF0OnUElCOtTTRc/edit?usp=sharing)

* *VMs require a Hypervisor* - The hypervisor is a software based
emulation layer for computer hardware and so it is generally slower
running software in a VM than natively, even with Intel Vf-X, Sun
GridEngine. Free hypervisors slow; commercial ones are expensive! VirtualBox
is common free one; VMWare Workstation is a commercial one.

* *Generally containers are used in command-line only* - With VMs it is very easy
to get a full desktop environment. With containers this is more difficult.
If we have time, may show a demo of this.

* *They take up much less space* - Virtual Machines have to bundle the whole operating system,
including components which would be the same on the host system. Containers, by virtue of using the
host system's kernel (at least on Linux), can therefore take up much less room.

### Potential Use Cases for Containers as a Scientist

Consider the following, which are all valid use cases:

* A new PhD student joins your lab. He isn't an experienced programmer, and setting
him up with all of the dependencies will take some time. Using a container means he can
get *all* of the dependencies and a copy of the software working on his computer in minutes.

* An old piece of software runs fine on Ubuntu, but a colleague hasn't been able to install
a necessary package because it's not available on Windows which is what he uses.

* You've just been given an Microsoft Azure Academic Grant, and you now want to run thousands of
copies of your research software in the cloud, and you want to avoid a complicated install process.

* You have a data analysis script that chugs away on your desktop for every set of simulation data you produce.
However, you run thousands of simulations per week, and the data analysis script takes some time to run. You might install
this script into a container, and use that as the basis for running the data analysis on a large cluster.
