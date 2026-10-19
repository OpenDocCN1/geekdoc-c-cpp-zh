![](bbox=[0.125, 0.12, 0.64, 0.38])

Figure 7.1 A graphical representation of the steps involved in solving for a zero of f(x) using the bisection algorithm. The bisection algorithm takes the midpoint of the interval as the new guess for x, and so each step reduces the interval size by one-half. Four steps are shown for the algorithm.

smaller and smaller intervals within which the zero lies. Other techniques, such as the Newton–Raphson method we describe next, may converge more quickly, but if the initial guess is not close, it may become unstable and fail completely.

The basis of the bisection algorithm is shown in Figure 7.1. We start with two values of x between which we know that a zero occurs. (You can determine these by making a graph or by stepping through different x values and looking for a sign change.) To be specific, let us say that f(x) is negative at x_- and positive at x_+ :

```
f(x_-) < 0,    f(x_+) > 0.    (7.5)
```

(Note that it may well be that x_- > x_+ if the function changes from positive to negative as x increases.) Thus, we start with the interval x_+ ≤ x ≤ x_- within which we know a zero occurs. The algorithm (implemented as in Listing 7.1) then picks the new x as the bisection of the interval and selects as its new interval the half in which the sign change occurs:

```
x = ( xPlus + xMinus ) / 2
if ( f(x) f(xPlus) > 0 ) xPlus = x
else xMinus = x
```

This process continues until the value of f(x) is less than a predefined level of precision or until a predefined (large) number of subdivisions occurs.