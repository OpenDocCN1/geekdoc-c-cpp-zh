# ### 7.5.1 Operations on Truncated Power Series

The ring Q[[x]] of formal power series is constructed by

```
    sage: R.<x> = PowerSeriesRing(QQ)
```

or in short R.<x> = QQ[[]]^5. The elements of A[['x']] are truncated power series, i.e., objects of the form

$$f = f_0 + f_1 x + ... + f_{n-1} x^{n-1} + O(x^n).$$

They play the role of approximations of infinite “mathematical” series, much like elements of RR are approximations of real numbers. The A[['x']] ring is thus an inexact ring.

Each series has its own order of truncation^6 and the precision automatically follows through computations:

```
    sage: R.<x> = QQ[[]]
    sage: f = 1 + x + O(x^2); g = x + 2*x^2 + O(x^4)
    sage: f + g
    1 + 2*x + O(x^2)
    sage: f * g
    x + 3*x^2 + O(x^3)
```

Series with infinite precision do exist, they correspond exactly to polynomials:

```
    sage: (1 + x^3).prec()
    +Infinity
```

A default precision is used when it is necessary to truncate an exact result. It is given at the ring creation, or afterwards with the set_default_prec method:

```
    sage: R.<x> = PowerSeriesRing(Reals(24), default_prec=4)
    sage: 1/(1 + RR.pi() * x)^2
    1.00000 - 6.28319*x + 29.6088*x^2 - 124.025*x^3 + O(x^4)
```

As a consequence of the above, it is not possible to test the mathematical equality between two series. This is an important difference between these objects and the other classes of objects seen in this chapter. Sage thus considers two elements of A[['x']] as equal as soon as they match up to the smallest of their precisions:

```
    sage: R.<x> = QQ[[]]
    sage: 1 + x + O(x^2) == 1 + x + x^2 + O(x^3)
    True
```

Warning: this implies that the test O(x^2) == 0 returns true.
The basic arithmetic operations on series work as for polynomials. We also have some usual functions, for example f.exp() when f(0) = 0, as well as the

^5 Or from Q[[x]], by QQ[['x']].completion('x').

^6 In some sense, this is the main difference between a polynomial modulo x^n and a series truncated at order n: the operations on these two objects are analogous, but the elements of A[[x]]/(x^n) have all the same "precision".