---
title: "Generating documentation with Sphinx"
date: 2018-10-26T22:07:04+01:00
draft: false
---

# Quick Notes

* Pip install sphinx rather than through apt-get because otherwise TZ settings do not work well

```Docker
from ubuntu:18.04
RUN apt-get update && apt-get install python3 python3-pip

RUN pip3 install


WORKDIR /app
```

Then
```bash
docker build . -t documentation
docker run -v `pwd`:/app -it documentation
sphinx-quickstart
```
* Most defaults are OK but:
  *  We want to set default document to markdown rather than RST
  *  We want to enable MathJax


* Now Edit conf.py:

Uncomment these lines of code in conf.py
```python

# If extensions (or modules to document with autodoc) are in another directory,
# add these directories to sys.path here. If the directory is relative to the
# documentation root, use os.path.abspath to make it absolute, like shown here.
#
# import os
# import sys
# sys.path.insert(0, os.path.abspath('.'))
```

  - to extensions add sphinx.extensions.doctest and sphinx.extensions.napoleon
  - napoleon allows NumPy style documentation
  - after extension declarations add following:

```python
napoleon_google_docstring = False

doctest_global_setup = """
from quicktest import *
"""
```


Then, from root dir:

```
sphinx-apidoc -s md -o source ../quicktest
make html
```
Note: -s flag changes suffix from rst autodoc to md autodoc.
source is output directory
quicktest is source code directory


* Create a file called tutorial.rst

```rst
Tutorial
========

This is a tutorial.

Subheading
----------

Here is some text under a subheading

```

In index, change the toctree (table of contents tree) to:

```rst
.. toctree::
   :maxdepth: 2
   :caption: Contents:

   tutorial
```

Now, 'make html'

You can see that the tutorial page has appeared in the documentation.


# Putting online

* Log in to RTD with GitHub acct

* Import Repository

* Select correct repo

* Click build

* Builds automatically
