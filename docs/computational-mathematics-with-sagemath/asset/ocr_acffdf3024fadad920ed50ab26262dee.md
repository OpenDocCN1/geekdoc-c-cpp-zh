# ### 14.1.2 Multiple Integrals

Let us consider the double integral:

$$I = \int_0^1 \int_0^{\sqrt{y}} \exp(y\sin x)\, dx\, dy.$$

We first try to reduce it to a simple integral, by looking for a closed form for the inner integral, which fails in this case:

```
```sage
sage: y = var('y'); integrate(exp(y*sin(x)), (x, 0, sqrt(y)))
integrate(e^(y*sin(x)), x, 0, sqrt(y))
```
```

Since Sage does not provide any functionality for multiple integrals, we rewrite the problem as $I = \int_0^1 f(y)\,dy$, where $f$ is a Sage function, itself calling a numerical integration method:

```
```sage
sage: f = lambda y: numerical_integral(lambda x: exp(y*sin(x)), \
...:                                     0, sqrt(y))[0]
sage: f(0.0), f(0.5), f(1.0)
(0.0, 0.8414895067661431, 1.6318696084180513)
```
```

We can now evaluate the integral of $f$ on $[0,1]$ numerically:

```
```sage
sage: numerical_integral(f, 0, 1)
(0.8606791942204567, 6.301207560882073e-07)
```
```

We might also use sage.calculus.calculus.nintegral to compute $f$:

```
```sage
sage: f = lambda y: sage.calculus.calculus.nintegral(exp(y*sin(x)), \
...:                                      x, 0, sqrt(y))[0]
sage: numerical_integral(f, 0, 1)
(0.860679194220456..., 6.301207560882096e-07)
```
```

or even mpmath.quad:

```
```sage
sage: f = lambda y: RDF(mpmath.quad(lambda x: mpmath.exp(y*mpmath.sin(x)), \
...:                                      [0, sqrt(y)]))
sage: numerical_integral(f, 0, 1)
(0.8606791942204567, 6.301207561187562e-07)
```
```

Note that mpmath is able to compute multiple integrals directly, even in arbitrary precision, however only on a rectangular domain:

```
```sage
sage: mpmath.mp.dps = 60
sage: f = lambda x, y: mpmath.exp(y*mpmath.sin(x))
sage: mpmath.quad(f, [0,1], [0,1])
mpf('1.28392205575238471754385917646324675741664250325189751108716305')
```
```

Sometimes, in particular when the integrand is expensive to compute, we want an answer with at most (say) $n^2$ evaluations, even if we get a worse accuracy of the result. Here is a solution using the options algorithm and max_points of numerical_integral: