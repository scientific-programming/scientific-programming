---
title: "Writing Complex Tests"
date: 2018-10-26T10:56:09+01:00
draft: false
weight: 32
---

### Convergence

Because of the ubiquity of differential equations in physical problems, it's a common exercise to calculate the numerical derivatives of functions. The truncation error on the derivative of an arbitrary function approximated as a central difference:

$$ f'(x) = \frac{f(x + h) - f(x - h)}{2h} + \mathcal{O}(h^2) $$

Check that the error on the derivative of the sine function converges as
