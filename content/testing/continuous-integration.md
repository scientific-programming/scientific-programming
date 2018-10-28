---
title: "Continuous Integration"
date: 2018-10-26T10:56:15+01:00
draft: false
---

### Continuous Integration

What is Continuous Integration?

* Runs the tests repeatedly, every time you make a change.
* You use a remote service, to avoid having to run all tests locally - useful if they take some time to run.
* Generally, CI services send you angry emails when tests fail!
* It requires you to be using version control, and all tests are run when you push your changes to the remote repository.
* If you are developing a new feature, tests also get run when you're developing features in a branch/fork.

There are a number of ways to do CI. If you don't have a server, and you're happy for your project to be hosted remotely on GitHub or on another site, you can use remote services such as TravisCI, CircleCI and GitLab. If you have your own server, and you need everything to be private (sometimes this is the case if you're working on academic work with industry partners), then there are services you can host locally such as Jenkins and Buildbot.

### TravisCI

We'll here pick this, as it’s easy to set up from what we’ve already done:

First, log in to [Travis CI](https://travis-ci.org/) with your GitHub account.

Now, to build our repository, we'll need to put a very simple Travis configuration file into the root of the Git repository. Create a file called '.travis.yml'. This is written in a markup language called YAML, but the syntax for this is very simple.

Travis comes preinstalled with many programming languages, but uses an older version of Ubuntu. Because we have used Docker throughout to run our software, however, we can just use this as the basis on Travis to run our software. We need to specify only a few options, and everything is set up for us:

```
sudo: required

services:
  - docker
```

These options just tell travis that root permissions are needed (a requirement for Docker itself), and we need Docker to be installed.

When Travis builds first start, they clone the latest commit from the Git repository, and then change directory into that folder. So from then on, you can write out commands referring to files in that folder.

So now, we want to get the right environment to run our tests. Let's build the Docker container from the Dockerfile in our repository. Add the following lines.

```
before_install:
  - docker build . -t build
```

The before_install section here tells Travis to run the bash command on the subsequent line. This is normally where you run any setup which is needed to run the tests.

Now, we've done everything we need to do before running the tests, so let's put in the command to run them. We do this in a 'script' block:

```
script:
  - docker run -v`pwd`:/io build pytest -v .
```

The total file should now look like:

```
sudo: required

services:
  - docker

before_install:
  - docker build . -t build

script:
  - docker run -v`pwd`:/io build pytest -v .
```

Stage this file in your Git repository and commit it. Push it to GitHub, then navigate to the Travis website again. You should now see that your repository has appeared, and that a build is in progress. If everything is correct, your Python tests should run remotely!

Clearly, we could have much more complex build processes than this, and you run Python inside the build environment rather than in a Docker container. However, it's in general a good idea to delegate these into a container, as it avoids you having to duplicate the install script in multiple places, and keeps the development environment where you work the same as the test environment.

### Showing this on GitHub.

One common thing to do is to add a readme file to a GitHub repository. Generally these just give some information for people who come across the project, such as install instructions. These files are typically written in Markdown - a simple syntax which is widely used online in forums and in many other places. A simple README.md, written in Markdown, for this project could be:

```markdown
# Testing and CI

This repository follows the material on https://scientific-programming.github.io
to create a repository with simple Python tests and Continuous Integration set up.
```

We can add a badge to this to show the status of the build (i.e. passing or failing). Go to the Travis page for your repository.

### Workflow

A normal workflow for continuous integration is often something like:

* Create a branch or a fork of a repository to work on a new feature.
* Write some tests, and run ones relevant to the changes you're making on your local machine.
* Commit changes, and push to the remote repository.
* If any tests fail, you'll get a notification of this, and you can fix them.

However, it can also be useful to set up tests to run at periodic intervals - i.e. nightly.
This means that if a dependency unexpectedly changes in a repository that you're not actively contributing to,
