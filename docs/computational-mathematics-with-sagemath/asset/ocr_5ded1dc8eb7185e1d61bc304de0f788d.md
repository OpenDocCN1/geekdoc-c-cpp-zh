Suppose we have constructed three approximations $r$, $s$, and $t$ of the solution to the equation $f(x)=0$. We consider the Lagrange interpolation polynomial defined by the three points on the graph of $f$ with $x$-coordinates $r$, $s$, and $t$. It is a second-degree polynomial. We take as new approximation the root of this polynomial that is closest to $t$. The first three terms of the sequence are just taken to be $a$, $b$, and $(a+b)/2$.

We should note that the roots of the polynomials — and hence the computed approximations — can be complex numbers.

The implementation of this method in Sage is not difficult; it can be done similarly to the secant method. However, our implementation uses a data structure that is better suited to enumerating the terms of a recursive sequence.

```
sage: from collections import deque
sage: basering = PolynomialRing(CC, 'x')
sage: def quadratigen(f, r, s):
.....:     t = (r + s) / 2
.....:     yield t
.....:     points = deque([(r,f(r)), (s,f(s)), (t,f(t))], maxlen=3)
.....:     while True:
.....:         pol = basering.lagrange_polynomial(points)
.....:         roots = pol.roots(ring=CC, multiplicities=False)
.....:         u = min(roots, key=lambda x: abs(x - points[2][0]))
.....:         points.append((u, f(u)))
.....:         yield points[2][0]
```

The module `collections` of the Python standard library provides several data structures. In `quadratigen`, the class `deque` is used to store the last approximations computed. A deque object stores data up to the limit `maxlen` specified at its creation; here the maximum number of stored data is the recurrence order of the sequence of approximations. Once a deque object reaches its maximum storage capacity, the method `deque.append()` inserts new data according to the rule “first in, first out”.

Note that the iterations of this method do not require the computation of derivatives. Moreover, each iteration only requires one evaluation of the function $f$.

```
sage: generator = quadratigen(f, a, b)
sage: iterate(generator, check=checkconv)
After 5 iterations: 2.15846852554764
```

**Back to Polynomials.** We return to the situation studied at the beginning of the chapter: compute the roots of a polynomial $P$ with real coefficients. We assume that $P$ is monic:

$$P = a_0 + a_1x + \cdots + a_{d-1}x^{d-1} + x^d.$$