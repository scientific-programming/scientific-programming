---
title: "Testing Scientific Code"
date: 2018-10-26T10:55:14+01:00
draft: false
weight: 30
---

### What is a software test?

Software tests are written in order to check that the implementation of software is correct, and to guard against dangerous behaviour. They're used to make software run in a safer manner; if we know what the inputs and outputs of sofware should be, and we know that for those inputs the answer is correct, we can have some confidence that the software is correct.


Why is this important? Consider how science works in experimental science. We try and apply the scientific method:

{{% panel theme="info" header="Scientific Method" %}}

A set of rough principles:

* Ask a question.
* Form a hypothesis.
* Make a prediction based on the hypothesis.
-   Design an experiment to test the hypothesis.
-   Build the equipment
-   **Calibrate equipment by testing it**
-   Run the experiment
-   Detail carefully the procedures and record information.
-   Draw conclusions from results.
{{% /panel %}}

Consider whether, when writing software to do science, you check that your 'equipment' is calibrated? In many cases, the answer will be no.

Why might this be the case? Often ad-hoc changes are made to code which mean things stop working. Have you ever come back to a script that you wrote and found it no longer works because you changed a file somewhere else? These issues become especially common when multiple people, who might not have oversight over what you are using it for, are working on software.

In this tutorial, we'll step through some examples in the Python language which aim to show how you can write tests, and incorporate them into your own software in practice.



### Starting off simply: Squaring a number

Consider as an example, a function which takes a number and computes the square of that number.

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


### Principles of Software Testing

-   Software must meet the requirements

-   Software must respond correctly to different inputs

-   Software must run in a reasonable amount of time

-   Can be installed and run in the intended environment

### Static vs Dynamic Testing

[Static Testing]{}

-   Reviews - Reviewing the code manually as a group.

-   Walthrough - Parties go through a products specification to give
    feedback on potential defects.

-   **Verification of design**

[Dynamic Testing]{}

-   Executing portions of the code and checking the response.

-   **Validation of design**

### Why is it difficult for science?

-   Much of the time you don’t know what the results will be.

-   Realistic problems can take time to run.

-

### Why is it crucial for science?

-   Often need to implement new algorithms or change things.

-   Changing without testing will break things.

-   You might need to come back to a previous experiment to use it as
    the basis for a new one; if the code is broken, you will have
    issues!

### Dynamic Testing: Types of Test

##### Unit Tests

-   Code is written in small, independent functions

-   Each function has tests that check that the result makes sense

-   For e.g. a test of a function that calculates sin could check
    $\sin{\left(n\pi\right)} = 0 \,\,\,\,\, \forall n \in \mathbb{Z}$

##### Integration Tests

-   Tests check that the system as a whole works convincingly.

-   For e.g. a test of a molecular dynamics code might test that the
    pressure is close to the expected value after some equilibrium time.

-   Much, much harder to design, but essential - can be written so that
    they also serve as examples of how to use the software.

##### Regression Tests

-   Check that results don’t get less accurate over time.

-   Check that performance stays the same or gets better over time.

### Aside: Test Driven Development

Methodology for testing where **tests are written before writing any
code**.

This means that...

* Before writing any code you need to plan out what the interface should be (i.e. what arguments get passed to functions).
* You must work out what the *output* should be before writing any code.
* Can form part of the ’agile’ methodology for software development.
* Can be difficult for developing scientific code where answers can be difficult to determine in advance.
