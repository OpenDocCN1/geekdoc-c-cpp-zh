# A.7 Polynomials

# Exercise 24 page 129.

+   1. For example, but there exist many other solutions, we can take

```
```sage
sage: x = polygon(QQ, 'y'); y = polygon(QQ, 'x')
```
```

Let us recall the difference, in Sage, between Python variables and mathematical variables. Python variables are names, used for programming; they only denote a position in the memory. The mathematical variables, and polynomials are part of them, are completely different by nature; they are Sage objects which *can be stored* in Python variables. If we create an indeterminate called `'x'`, we are not forced to store it in the Python variable x — and we can also store `'y'` there.

+   2. We first assign the indeterminate `'x'` of the polynomials with rational coefficients to the Python variable x. Then, the expression `x+1` evaluates as the polynomial $x+1 \in \mathbb{Q}[x]$ which we assign to the variable p. After that we assign the integer 2 to the variable x. This operation has no effect on p, which keeps the value $x+1$; this x is the indeterminate; it has nothing to do with the Python variable whose value is now 2. Now `p+x` evaluates as $x+3$, and thus, the final value of p is $x+3$.

# Exercise 25 page 135.

A simple solution is to carry out successive Euclidean divisions by the Chebyshev polynomials by increasing powers: if the polynomial degree is $n$, we set $p = c_n T_n + R_{n-1}$ with $c_n \in \mathbb{Q}$ and $\deg R_{n-1} \le n-1$, then $R_{n-1} = c_{n-1}T_{n-1}$ and so on.

In the Sage program below, instead of returning the computed coefficients $c_n$ as a simple list, we prefer to build a symbolic expression where the polynomial $T_n$ is represented as an “inert” function (that is to say in a non-evaluated form) `T(n,x)`.

```
```sage
sage: T = sage.symbolic.function_factory.function('T', nargs=2)
sage: def to_chebyshev_basis(pol):
....:     (x,) = pol.variables()
....:     res = 0
....:     for n in xrange(pol.degree(), -1, -1):
....:         quo, pol = pol.quo_rem(chebyshev_T(n, x))
....:         res += quo * T(n, x)
....:     return res
```
```

Let us test this function. To check the results, we can just substitute the function which computes the Chebyshev polynomials into our “inert” function T, and then expand the result:

```
```sage
sage: p = QQ['x'].random_element(degree=6); p
4*x^6 + 4*x^5 + 1/9*x^4 - 2*x^3 + 2/19*x^2 + 1
sage: p.ch = to_chebyshev_basis(p); p.ch
1/8*T(6, x) + 1/4*T(5, x) + 55/72*T(4, x) + 3/4*T(3, x) + 27/1368*T(2, x) + T(1, x) + 1069/456*T(0, x)
```
```