---
title: "Writing Simple Tests"
date: 2018-10-26T10:56:09+01:00
draft: false
weight: 33
---

#### Set up

For this workshop, build the following Dockerfile, and label it 'testing'. Pip is a package manager for Python; using it, we can install Python libraries.

```docker
from ubuntu:18.04

RUN apt-get update && apt-get install -y python3 python3-pip

RUN pip install numpy matplotlib

WORKDIR /app
```


#### Starting off simply: Normalising a vector

Consider as a really simple example, a function which normalises a vector. We're going to start and thing about how it should work.

If there are n elements in a vector, the norm is given by:
$$\sqrt{x_1^2 + x_2^2 + x_3^2 + x_4^2 + \cdot + x_n^2}$$

Various appropriate tests of this could check:

* If we pass an array full of integers or floating point numbers, do we get the correct answer?
* If we pass an array which is full of zeros?
* How does the function behave when an input argument is not of the type specified is passed in (such as a string)?

Now we've thought about what we ought to test, we can write a test. In Python, the way to do this is to preface the name of a function with "test_". Create a


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

Most programming languages have the concept of exceptions. An exception is just a way of dealing erroneous conditions which happen while a programme is running which require special handling. In Python doing this in your own code is really straightforward. For example, when calculating the Coulomb potential in 1-D, we need to make sure that if the input distance is zero, the function raises an error, because the input argument is invalid. We can do this like:

```
def CoulombPotential(r):
    if (r == 0):
        raise ValueError("r cannot equal zero.")
    return 1 / abs(r)
```

Now, when we run this code, if 0 is passed as an input argument:


```python
>>> CoulombPotential(0)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in CoulombPotential
ValueError: r cannot equal zero.
```



### Debug Mode

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

We can see that the print statement is completely skipped, and instead of our helpful error message which resulted from our check, we get Python's less helpful one.

{{% panel theme="info" header="C, C++ and FORTRAN Compilers" %}}
Achieving the same in compiled languages is also straightforward, because a preprocessor runs over the code before the compilation stage when a compiler is invoked. Macros can be used to disable code under certain conditions, and this is widely used to disable costly code paths that diagnose errors, which can be turned on when an issue is noticed. See for example the following code which multiplies two vectors in C++:

```c++
void multiply_vector(const std::vector<double> a,
                     double b,
                     std::vector<double> &c) {

  for(int i = 0; i < a.size(); i++) {
    c[i] = a[i] * b;
    #ifdef MYPROJECT_DEBUG
    std::cout << "c[" << i << "] = " << c[i] << std::endl;
    #endif
  }
}
```

Compiling with g++, you can enable the printing of the array in this function just by passing a flag:

```g++
g++ file.cpp -DMYPROJECT_DEBUG
```
{{% /panel %}}

### Try and Except

We've already shown how to raise errors under particular conditions.


### Exercise 1: Write a first function and test

The Lennard-Jones potential is given by $$ V\left(r\right) = \epsilon \left[\left(\frac{r_m}{r}\right)^{12} - 2\left(\frac{r_m}{r}\right)^6\right]$$

* Write a function that takes three numbers - $$\epsilon$$, $$r_m$$ and $$r$$, and returns this potential.

* Write a test for this function which checks the values.
* Write a test that checks that the function throws a ValueError if numerical arguments are not passed.


### Exercise 2: Normalise a vector

Write a function which takes a numpy array of arbitrary length:

```
import numpy as np


a = np.array([1.0, 2.0, 3.0])
```

and returns
