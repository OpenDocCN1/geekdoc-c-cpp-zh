![](bbox=[0.2, 0.078, 0.77, 0.203])

Figure 2.1 – Two symbolic expressions representing the same mathematical object.

The most common operation consists of *evaluating* an expression by giving a value to some of its parameters. The subs method — which can be made implicit — performs this transformation:

```
sage: a, x = var('a, x'); y = cos(x+a) * (x+1); y
(x + 1)*cos(a + x)
sage: y.subs(a=-x); y.subs(x=pi/2, a=pi/3); y.subs(x=0.5, a=2.3)
x + 1
-1/4*sqrt(3)*(pi + 2)
-1.41333351100299
sage: y(a=-x); y(x=pi/2, a=pi/3); y(x=0.5, a=2.3)
x + 1
-1/4*sqrt(3)*(pi + 2)
-1.41333351100299
```

Compared to the usual mathematical notation `x ↦ f(x)`, the variable which is substituted must be explicitly given. The substitution of several parameters is done in parallel, while successive substitutions are performed in sequence, as shown by the two examples below:

```
sage: x, y, z = var('x, y, z'); q = x*y + y*z + z*x
sage: bool(q(x=y, y=z, z=x) == q), bool(q(z=y)(y=x) == 3*x^2)
(True, True)
```

To replace an expression more complex than a single variable, the `substitute` method is available:

```
sage: y, z = var('y, z'); f = x^3 + y^2 + z
sage: f.substitute(x^3 == y^2, z==1)
2*y^2 + 1
```

# 2.1.2 Transforming Expressions

The simplest non-constant expressions are polynomials and rational functions of one or more variables. The functions allowing to rewrite expressions in several forms or to put them in normal form are summarised in Table 2.1. For example, the expand method is useful to expand polynomials:

```
sage: x, y = SR.var('x,y')
```