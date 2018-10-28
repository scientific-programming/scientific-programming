---
title: "Writing Complex Tests"
date: 2018-10-26T10:56:09+01:00
draft: false
weight: 32
---

### Principles of Software Testing

What are the main principles of software testing? Generally, people don't start out writing software with no idea what it should do - they should have some idea of the requirements. The written software must then:

-   Meet the original requirements
-   Must respond correctly to different inputs
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
