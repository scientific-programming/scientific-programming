---
title: "Documenting Code"
date: 2018-10-26T22:07:04+01:00
draft: false
weight: 41
---

#### Writing some documentation

There are a number of different tools for automatically generating documentation
for different languages. For Python, a common tool is [Sphinx](http://www.sphinx-doc.org/en/stable/).
For projects which combine several languages, sometimes the tool [Doxygen](http://www.doxygen.org/) is preferred.

Here, we'll focus on Sphinx, but generally all tools work by similar principles;
the source code of a library is parsed, and the author of code annotates it
in order to provide the documentation.

In Python, we can document a function with a documentation string, or 'docstring.'
These are provided as a multi-line string just under the function signature in
the source code.

Consider our simple 'squared' and 'power' functions from the testing tutorial:

```python3
def squared(x):
    return x * x

def power(x, n):
    return x ** n
```

An annotated version of 'squared', using the NumPy documentation standard, could be:

```python3
def squared(x):
    """
    Returns the square of the input x

    Parameters:
    -----------
    x, float:
       Base number

    Returns:
    --------
    float:
       Base number raised to power 2

    See Also:
    ------
    pow : raise an argument to an arbitrary power

    Examples
    --------

    >>> squared(2)
    4

    >>> squared(8)
    64

    >> squared(-1)
    1
    """
    return x*x
```

This might seem verbose, but, everything that's needed is there.

### Accessing the documentation from Python


{{% panel theme="info" header="Accessing Documentation from Python" %}}

If you're in a Python interpreter, you can access the documentation by calling the
help function with the name of the function or class you're interested in:
```python
>>> help(function_name)
```

{{% /panel %}}
