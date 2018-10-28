---
title: "Documentation"
date: 2018-10-26T10:58:18+01:00
draft: false
weight: 50
---

### What makes good documentation on a software project?

Nothing can frustrate a user more than coming across a project which has inadequate documentation; without a knowledge of the underpinnings of a software library, the user must either field questions to the authors if they, indeed, are able to take them, or begin to study the source code in detail. This, however, causes many problems. Perhaps the user has no expertise in the area they wish to look at, and the source code is beyond their understanding. It may be that they get so frustrated that they begin to reimplement parts of a library themselves, to avoid having to work with code that they have not written. A piece of software may provide the most elegant solutions in the world for a particular problem, but if users find that they are unable to work with it through a lack of understanding about what the constituent parts do, it is unlikely to see much uptake.

### What makes good documentation?

There are broadly two types of documentation for software libraries:

* API Documentation - This describes all of the functions that are usable, specifying the input arguments, the behaviour of the function and the return values.

* Examples - Providing examples in context, which show how to use the particular functions, showing particular input values explicitly and what the results are.

In general, the best software documentation contains both detailed documentation of the API and examples along with it. Why is this the case?

If you want to quickly use a library, and know roughly what you're looking for, examples are normally the quickest way to get started. On the other hand, if you need to use more sophisticated features of a library, you're likely to need the API documentation, because it gives more details of the 'advanced' features. A good rule of thumb when writing documentation is that examples should try and show 'enough' - if there are any pitfalls that might be non-obvious, it's better to point these out and save users any pain.

Perhaps the best way to learn what software documentation should look like is the use and study of projects which are well documented. We'll look here at an example from the the Python library SciPy.

#### Newton Raphson documentation

Consider the [Newton-Raphson algorithm](../testing/complex-tests/) we used as an example in the testing section of these tutorials. The iterative procedure for finding the root of a function is given by:

$$
x\_{n+1} = x\_{n} - \frac{f(x\_n)}{f'(x\_n)}
$$

Because this is such a ubiquitous method, it's a good one for us to consider when looking at documentation.

Let's take a look at the [SciPy documentation for this function](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.newton.html). The descriptions of the parameters in the whole of the SciPy library (and also the NumPy library) are written to a set of standards. These standards are defined in the documentation [here](https://www.numpy.org/devdocs/docs/howto_document.html#docstring-standard), and they are worth a read to anyone writing software as they are something of a gold standard. Indeed, many other Python projects implement documentation in the same format as these libraries. Here we'll just discuss briefly the main features:

We can see first that it starts first with the function signature (i.e. the input arguments), and both a brief and long form description:

```
scipy.optimize.newton(func, x0, fprime=None, args=(),
tol=1.48e-08, maxiter=50, fprime2=None)
Find a zero using the Newton-Raphson or secant method.

Find a zero of the function func given a nearby starting point x0. The
Newton-Raphson method is used if the derivative fprime of func is provided,
otherwise the secant method is used. If the second order derivative fprime2 of
func is provided, then Halley’s method is used.
```

The function signature tells us the input arguments, but without some thought, it would still be difficult to immediately use the function. The description tells us the key information about the particular function, and a bit of brief clarifying information about the function. The key parts, however, are really what follow:
```

Parameters:
func : function
  The function whose zero is wanted. It must be a function of a single variable
  of the form f(x,a,b,c…), where a,b,c… are extra arguments that can be passed
  in the args parameter.

x0 : float
  An initial estimate of the zero that should be somewhere near the actual zero.

fprime : function, optional
  The derivative of the function when available and convenient. If it is None
  (default), then the secant method is used.

args : tuple, optional
  Extra arguments to be used in the function call.

tol : float, optional
  The allowable error of the zero value.

maxiter : int, optional
  Maximum number of iterations.

fprime2 : function, optional
  The second order derivative of the function when available and convenient. If
  it is None (default), then the normal Newton-Raphson or the secant method is
  used. If it is not None, then Halley’s method is used.

Returns:
  zero : float
  Estimated location where function is zero.
```

Each input and output parameter has its type specified - especially necessary in Python given that it is a dynamically-typed language. Some parameters, which are optional, are stated as such. We note that the default values for the optional arguments were given above in the function signature. Then, following each parameter is a description of the input parameters.

Following these, examples are given on how to use the function:
```python
>>> def f(x):
...     return (x**3 - 1)  # only one real root at x = 1
>>>
>>> from scipy import optimize
# fprime not provided, use secant method

>>>
>>> root = optimize.newton(f, 1.5)
>>> root
1.0000000000000016
>>> root = optimize.newton(f, 1.5, fprime2=lambda x: 6 * x)
>>> root
1.0000000000000016
# Only fprime provided, use Newton Raphson method

>>>
>>> root = optimize.newton(f, 1.5, fprime=lambda x: 3 * x**2)
>>> root
1.0
# Both fprime2 and fprime provided, use Halley’s method

>>>
>>> root = optimize.newton(f, 1.5, fprime=lambda x: 3 * x**2,
...                        fprime2=lambda x: 6 * x)
>>> root
1.0
```

Note that several different perturbations of the input arguments are given. For most people, it would be enough to briefly look at the examples here, and they would immediately be able to get started with using the code.

What's particularly invaluable here is that both the function API documentation and the examples are given *in the same place*. This makes it quick to get started with using the code. In contrast, many software libraries provide examples and the API, but separate from each other.
