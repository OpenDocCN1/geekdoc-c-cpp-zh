The function $f(x) = 1/x$ can, course, be integrated analytically to give $\ln(x)$, and because $\ln(1) = 0$, the value of the integral is $\ln(2) = 0.6931478$. The trapezoidal approximation to the integral with $a=1$ and $b=2$ begins with Equation 14.6 to obtain $T_0$:

```
$T_0 = \frac{1}{2}\left(1 + \frac{1}{2}\right)(2 - 1) = 0.75$
```

Repeated use of Equation 14.11 yields the following:

```
$k = 1\n\Delta x_1 = 1/2\n$T_1 = T_0/2 + \Delta x_1[f(1 + \Delta x_1)] = 0.75/2 + 1/2(1+1/2) = 0.708333$
```

```
$k = 2\n\Delta x_2 = 1/4\n$T_2 = T_1/2 + \Delta x_2(1/1.25 + 1/1.75) = 0.6970238$
```

```
$k = 3\n\Delta x_3 = 1/8\n$T_3 = T_2/2 + \Delta x_3(1/1.25 + 1/1.375 + 1/1.625 + 1/1.875) = 0.69412185$
```

Continuing the calculation through $k=5$ yields the:

| k | $T_k$ |
| 0 | 0.75 |
| 1 | 0.708333 |
| 2 | 0.69702 |
| 3 | 0.69412 |
| 4 | 0.69339 |
| 5 | 0.693208 |
| . | . |
| Exact | 0.693147... . |

The convergence of the computed values of the trapezoidal rule isn't particularly fast, the method is quite simple.

# EXERCISES 14.6

+   1. (Practice) Evaluate the following integrals by using the trapezoidal rule:
   a. Evaluate $T_0$ for one panel by using Equation 14.6.