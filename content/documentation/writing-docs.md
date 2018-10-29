---
title: "Sphinx: Python documentation"
date: 2018-10-26T22:07:04+01:00
draft: true
weight: 43
---

# Installing Sphinx

We'll start with a Docker container (again!). Build the following:

```docker
from ubuntu:18.04

ENV TZ "Europe/London"
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y python3 python3-pip python3-sphinx

WORKDIR /app
```

with the command:

```bash
docker build . -t sphinx
```

Note that we've had to add some timezone information into the container here; don't worry too much about this.

Now, go to the repository in which you have your Python files.
