```
sage: desolve(DE, y).expand()
1/2*x^2 + C*e^(-2*x) - 3/2*x + 9/4
```

It is thus convenient to use the form `desolve(...).expand()`. Let us check which method has been used:

```
sage: desolve(DE, y, show_method=True)[1]
'linear'
```

Let us add an initial condition, for instance y(0) = 1:

```
sage: desolve(DE, y, ics=[0,1]).expand()
1/2*x^2 - 3/2*x - 5/4*e^(-2*x) + 9/4
```

# Separable Equations.

Let us solve y′ log(y) = y sin(x):

```
sage: x = var('x'); y = function('y')(x)
sage: desolve(diff(y,x)+log(y) == y*sin(x), y, show_method=True)
[1/2*log(y(x))^2 == _C - cos(x), 'separable']
```

Sage agrees with us: it is a separable equation.
We should assign the solutions in order to use them later on:

```
sage: ed = desolve(diff(y,x)+log(y) == y*sin(x), y); ed
1/2*log(y(x))^2 == _C - cos(x)
```

Here, y(x) is not explicitly given: 1/2 log²(y(x)) = _C − cos(x).
We can get y(x) explicitly using solve. Be aware that ed is an equation where y is a variable:

```
sage: solve(ed, y)
[[y(x) == e^(-sqrt(2*_C - 2*cos(x))), y(x) == e^(sqrt(2*_C - 2*cos(x)))]]
```

We should take care that sqrt(2*_C - 2*cos(x)) may cause some problems even if Sage does not warn us. We will then assume that _C ≥ 1.
To draw the graph of solutions, we need their right-hand side. For instance, in order to get the first solution’s right-hand side with _C = 5, we could type:

```
sage: solve(ed, y)[0].substitute(_C==5).rhs()
Traceback (most recent call last):
...
NameError: name '_C' is not defined
```

_C has not been defined but only introduced by Sage. We can get it through the variables() command which gives the variables list:

```
sage: ed.variables()
(_C, x)
```

Only _C and x are variables, y having been defined as a function of the variable x.

```
sage: c = ed.variables()[0]
sage: solve(ed, y)[0].substitute(c == 5).rhs()
e^(-sqrt(-2*cos(x) + 10))
```