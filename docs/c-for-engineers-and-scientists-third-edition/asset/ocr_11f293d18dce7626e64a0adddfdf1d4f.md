# Chapter 14 Refinements to the Bisection Method 761

# 14.3 Refinements to the Bisection Method

The bisection method described in Section 14.2 presents the basics on which most root-finding methods are constructed. This brute-force method is rarely used in practice because for almost any, an alternative method that's faster, more accurate, and only slightly more complex is available. All refinements of the bisection method that might be devised on attempts to use as much information as available as the function's behavior at each iteration. In the ordinary bisection method, the only feature of the function that's monitored is its sign. Therefore, if you're searching for roots of the function

```
$f(x) = e^x - \sin(\sqrt{2}\pi x)$
```

you begin the search, in Section 14.1, by stepping along the x-axis and watching for a change in sign of the function, follows:

| i | x_i | f(x_i) |
|---|---|--|
| 0 | 0.0 | 2.0 |
| 1 | 0.1 | 1.33 |
| 2 | 0.2 | 0.75 |
| 3 | 0.3 | 0.29 |
| 4 | 0.4 | -.05 |

The next step in the bisection method is reducing the step size by half; that is, $x_5 = 0.35$. However, from the magnitude of the preceding numbers, you would expect the root to be closer to 0.4 than 0.3. Using information about the size of the functional value in addition to its sign, you can speed up the convergence. In this example, you might interpolate the root to be approximately

> $\frac{0.29 - 0.0}{f_3 - f_4} = 0.853$

of the distance $x_3 = 0.3$ to $x_4 = 0.4$ or $x_5 = 0.3853$. Continuing in this manner and interpolating at each step, you get the following results:

| i | x_i | f(x_i) |
|---|---|--|
| 3 | 0.30 | 0.29 |
| 4 | 0.40 | -0.05 |
| 5 | 0.385 | -0.0083 |
| 6 | 0.3823 | -0.0013 |
| 7 | 0.3819 | -0.00019 |
| 8 | 0.38185 | -0.000028 |
| 9 | 0.38184 | -0.000004 |

Comparing these results with the bisection method applied to a similar function in Section 14.2, you can see that the convergence rate for this method is much faster. The next task is to formalize this procedure into a method suitable for a general function.