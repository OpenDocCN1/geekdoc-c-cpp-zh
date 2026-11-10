```
```sage
sage: alpha, m, x = var('alpha, m, x'); q = function('q')(x)
sage: p = (x - alpha)^m * q
sage: p.derivative(x)
(-alpha + x)^(m - 1)*m*q(x) + (-alpha + x)^m*diff(q(x), x)
sage: simplify(p.derivative(x)/(x-alpha))
0
```
```

Therefore, the gcd of $p$ and $p'$ is the product $\prod_{\alpha\in\Gamma}(x-\alpha)^{m_\alpha-1}$, where $\Gamma$ is the set of roots of $p$ with multiplicity strictly greater than 1, and $m_\alpha$ is the multiplicity of the root $\alpha$. If $d$ denotes this gcd, then the quotient $p/d$ has the desired properties.

Note that the degree of the quotient of $p$ by $d$ is strictly less than the degree of $p$. In particular, if this degree is strictly less than 5, it is possible to express the roots in terms of radicals. The following example illustrates this for a polynomial of degree 13 with rational coefficients.

```
```sage
sage: R.<x> = PolynomialRing(QQ, 'x')
sage: p = 128 * x^13 - 1344 * x^12 + 6048 * x^11 - 15632 * x^10 \
.....: + 28056 * x^9 - 44604 * x^8 + 71198 * x^7 - 98283 * x^6 \
.....: + 105840 * x^5 - 101304 * x^4 + 99468 * x^3 - 81648 * x^2 \
.....: + 40824 * x - 8748
sage: d = gcd(p, p.derivative())
sage: (p // d).degree()
4
sage: roots = SR(p // d).roots(multiplicities=False)
sage: roots
[1/2*I*sqrt(3)*2^(1/3) - 1/2*2^(1/3),
 -1/2*I*sqrt(3)*2^(1/3) - 1/2*2^(1/3),
 2^(1/3),
 3/2]
sage: [QQbar(p(alpha).is_zero() for alpha in roots]
[True, True, True, True]
```
```

# 12.2 Numerical Solution

There is a traditional dichotomy in mathematics between the *discrete* and the *continuous*. Numerical analysis bridges this gap to some extent: a major aspect of numerical analysis is the study of questions about real numbers (firmly part of the continuous domain) via an experimental point of view, often assisted by a computer, which belongs to the discrete domain.

Regarding the solution of non-linear equations, numerous natural questions arise beyond the computation of approximate values: how many real roots does a given equation have? How many imaginary, positive, or negative roots are there?

In this section we start to answer such questions in the special case of algebraic equations. Then we describe some of the methods for computing approximate solutions of a non-linear equation.