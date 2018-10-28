---
title: "Writing Simple Tests"
date: 2018-10-26T10:56:09+01:00
draft: false
weight: 10
---


#### Starting off simply: Squaring a number

Consider as a really simple example, a function which takes a number and computes the square of that number.

```python
def square(x):
    return x * x

```

Various appropriate tests of this could check:

* Is the correct answer given for positive integers?
* Is the correct answer given for negative integers?
* Is the correct answer given for zero?
* Is the correct answer given for positive and negative decimals?
* What is the behaviour for complex numbers?
* How does the function behave when an input argument is not of the type specified is passed in (such as a string)?

It's clear that all of these would be sensible, but considering it carefully, it shows immediately the difficulty of actually applying testing in practice. There are an infinite amount of numerical input arguments - we cannot reasonably test them all.

How can we therefore reduce it down to a more manageable set of tests? We by necessity have to restrict our tests to a subset of all of the possible outcomes, and have to exercise some thought.

In Python, we can write tests using the Pytest framework. Pytest goes through all of the files in a directory with a ".py" file extension, and looks for normal Python functions which have names that start with "test". It then runs all of these functions in sequence.

In general, it's a good idea to write tests in a separate file to the function implementation.

So, to keep track of what we're doing, we'll create a new folder and a new Git repository:

```
mkdir python-testing-tutorial
cd python-testing-tutorial
git init
```

In this folder, we'll create 'functions.py' and 'test_functions.py'

In functions.py add the function from above.

Now, in test_functions.py, we'll write a test. As mentioned before, you write a normal Python function. However, we use something that you may not have seen before - the assert statement:

```python
def test_square_positive_integers():
    assert square(1) == 1
    # Note the mistake here! We'll leave this here to
    # show what happens when a test fails.
    assert square(2) == 8
    assert square(4) == 16
    assert square(100) == 10000
```

Now, using our Docker knowledge from before, we're going to run this test with Python from a container. Create a Dockerfile with the following contents:

```docker
from ubuntu:18.04

RUN apt-get update
RUN apt-get install -y python3
RUN pip3 install pytest

WORKDIR /io
```

Here, we're using Pip, the Python package installer to install the Python package pytest.

Build the container:
```bash
docker build . -t python-testing
```

Now, we can run the tests with:

```bash
docker run -v`pwd`:/io python-testing pytest -v .
```

You should see output something like this:
```bash
============================= test session starts ==============================
platform linux -- Python 3.6.6, pytest-3.9.2, py-1.7.0, pluggy-0.8.0 -- /usr/bin/python3
cachedir: .pytest_cache
rootdir: /io, inifile:
collecting ... collected 1 item

test_functions.py::test_square_positive_integers FAILED                  [100%]

=================================== FAILURES ===================================
________________________ test_square_positive_integers _________________________

    def test_square_positive_integers():
        assert square(1) == 1
        # Note the mistake here! We'll leave this here to
        # show what happens when a test fails.
>       assert square(2) == 8
E       assert 4 == 8
E        +  where 4 = square(2)

test_functions.py:10: AssertionError
=========================== 1 failed in 0.16 seconds ===========================
```

Note now, that we can see that a test has failed where we introduced the error in the test. We can now correct the test so that it's expecting the correct answer:

```python
def test_square_positive_integers():
    assert square(1) == 1
    assert square(2) == 4
    assert square(4) == 16
    assert square(100) == 10000
```

Now if we rerun pytest, we see something different:
```bash
============================= test session starts ==============================
platform linux -- Python 3.6.6, pytest-3.9.2, py-1.7.0, pluggy-0.8.0 -- /usr/bin/python3
cachedir: .pytest_cache
rootdir: /io, inifile:
collecting ... collected 1 item

test_functions.py::test_square_positive_integers PASSED                  [100%]

=========================== 1 passed in 0.21 seconds ===========================
```

As many tests as are necessary can be written.

### Exceptions

Most programming languages have the concept of exceptions. An exception is just a way of handling conditions which happen while a programme is running which require special handling.


### Aside: Debug Mode

Many people do not know that the Python interpreter runs in 'debug' mode by default. When it is disabled, by running Python with the '-O' flag, all asserts are skipped, and the flag '__debug__' is set to True. Utilising this can be useful when you want to check code for correctness, but know that some checks you are running can be costly in performance. It can also be used to provide more


```python
def square(x):
  if __debug__:
    print("We're in debug mode!")
  assert type(x) in [int, float, complex], "Input argument x is not of a numeric type int, complex or float"
  return x*x
```

In debug mode, if we run the function, we get the following output:
```
>>> square(2)
We're in debug mode!
4
>>> square('a')
We're in debug mode!
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 4, in square
AssertionError: Argument is not of a numeric type
```

When we instead run 'python3 -O', we see:

```
>>> square(2)
4
>>> square('a')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 5, in square
TypeError: can't multiply sequence by non-int of type 'str'
```

We can see that the print statement is completely skipped, and instead of our helpful error message which resulted from our check, we get Python's slightly less helpful one.

### Exercise: Write a first function and test

The Couloumb potential is given by $$ V\left(r\right) = \frac{q}{|r|} $$

* Write a function that takes two parameters, x and q, and returns this potential.

* Write a test for the function, and

Note: The power operator in Python is "**", so to take the square root:

```python3
>>> 4 ** 0.5
2
```
