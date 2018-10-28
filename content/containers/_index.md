---
author:
- Ryan Pepper
date: October 29th 2018
title: 'Containers'
draft: false
weight: 30
---

### What are containers?
-  Mechanism for setting up environment
-  Allows control of dependencies
-  Describes setup process through scripting in standardised manner
-  Can be easily distributed to other developers (binary vs script)
-  Not a virtual machine (in most cases...)

### What are containers not?
-  Not the best way to *distribute* software, especially in scientific use cases.
-  An excuse not to write down strict dependency requirements for your software (e.g. versions of libraries).
-  A way of avoiding updating scientific software because it now runs everywhere.

### Terminology
-   Host - Computer running VM/container.
-   Image - Binary file
-   Hypervisor - software running VM.
-   Kernel - Core OS components

###  Comparisons with Virtual Machines
####  How are containers like VMs?

* *Isolated environment* - Processes run isolated from other processes -
they can’t access hardware resources they aren’t allocated.
* *They are independent* - Generally you can be given a container image or
a virtual machine image and use that to run a piece of software without
doing anything else.

### How are containers not like VMs?
* *They use Kernel features of the host*  Linux supports process and
resource partitioning and isolation (cgroups, OverlayFS, kernel
namespacing), which allows containers to use a subset of resources.

* *VMs require a Hypervisor* The hypervisor is a software based
emulation layer for computer hardware and so it is generally  20% slower
running software in a VM than natively, even with Intel Vf-X, Sun
GridEngine. Free hypervisors slow; commercial are expensive!

* *Generally containers are command-line only* With VMs it is very easy
to get a full desktop environment. With containers this use case is generally not
well supported.

* *They take up much less space* Virtual Machines have to bundle the whole operating system,
including components which would be the same on the host system. Containers, by virtue of using the
host system's kernel (at least on Linux), can therefore take up much less room.


### Potential Use Cases for Containers

* A new PhD student joins your lab. He isn't an experienced programmer, and setting
him up with all of the dependencies will take some time. Using a container means he can
get *all* of the dependencies and a copy of the software working on his computer in minutes.

* An old piece of software runs fine on Ubuntu, but a colleague hasn't been able to install
a necessary package because it's not available on Windows which is what he uses.

* You've just been given an Microsoft Azure Academic Grant, and you now want to run thousands of
copies of your research software in the cloud, and you want to avoid a complicated install process.

* You have a data analysis script that chugs away on your desktop for every set of simulation data you produce.
You want to run it on your Universities HPC cluster, but you're not sure how to compile all of the dependencies
from source, which is what you'd need to do otherwise.
