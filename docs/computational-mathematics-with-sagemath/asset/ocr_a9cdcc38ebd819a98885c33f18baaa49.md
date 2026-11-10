# First-Order Equations Directly Solved by Sage.

We will study in this section how to solve with Sage linear, separable, Bernoulli, Riccati, Lagrange, Clairaut, homogeneous and exact equations.

Linear equations. These are equations of the form

$$y' + P(x)y = Q(x),$$

where $P$ and $Q$ are continuous functions on given intervals.

Example: $y' + 3y = e^x$.

```
```sage
x = var('x'); y = function('y')(x)
```
```

```
```sage
desolve(diff(y,x) + 3*y == exp(x), y, show_method=True)
[1/4*(4*_C + e^(4*x))*e^(-3*x), 'linear']
```
```

Separable equations. These are equations of the form

$$P(x) = y'Q(y),$$

where $P$ and $Q$ are continuous functions on given intervals.

Example: $yy' = x$.

```
```sage
desolve(y*diff(y,x) == x, y, show_method=True)
[1/2*y(x)^2 == 1/2*x^2 + _C, 'separable']
```
```

Caution! Sometimes Sage solves separable equations as exact. Example: $y' = e^{x+y}$.

```
```sage
desolve(diff(y,x) == exp(x+y), y, show_method=True)
[-(e^(x + y(x)) + 1)*e^(-y(x)) == _C, 'exact']
```
```

Bernoulli equations. These are equations of the form

$$y' + P(x)y = Q(x)y^\alpha,$$

where $P$ and $Q$ are continuous functions on given intervals and $\alpha \notin \{0,1\}$. Example: $y' - y = xy^4$.

```
```sage
desolve(diff(y,x)-y == x*y^4, y, show_method=True)
[e^x/(-1/3*(3*x - 1)*e^(3*x) + _C)^(1/3), 'bernoulli']
```
```

Homogeneous equations. These are equations of the form

$$y' = \frac{P(x,y)}{Q(x,y)},$$

where $P$ and $Q$ are homogeneous functions of same degree on given intervals.

Example: $x^2y' = y^2 + xy + x^2$.

```
```sage
desolve(x^2+diff(y,x) == y^2+2*x*y+x^2, y, show_method=True)
```
```