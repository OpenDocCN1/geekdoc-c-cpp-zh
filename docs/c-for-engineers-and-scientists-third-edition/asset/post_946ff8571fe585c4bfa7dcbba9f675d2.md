
# Chapter 14

## The Secant Method

# Program 14.3

```cpp
#include <iostream>
#include <cmath>
using namespace std;

void secant(double, double, double, int); // function prototype
double f(double); // function prototype

int main()
{
    int imax; // maximum number of iterations
    double a, b; // left and right ends of the original interval
    double epsilon; // convergence criterion

    // obtain the input data
    cout << "Enter the limits of the original search interval, a and b: ";
    cin >> a >> b;
    cout << "Enter the convergence criteria: ";
    cin >> epsilon;
    cout << "Enter the maximum number of iterations allowed: ";
    cin >> imax;

    secant(a, b, epsilon, imax);

    return 0;
}

// This function implements the secant method for finding
// a root of a function
void secant(double a, double b, double epsilon, int imax)
{
    int i; // current iteration counter
    double x0, x1; // left and right x values of current interval
    double f0, f1; // function evaluated at these points
    double dx0; // delta x0
    double dx1; // delta x1
```

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_790_0.png)

```cpp
// echo back the passed input data
cout << "\nThe original search interval is from " << a << " to " << b
 << "\nconvergence criterion is: interval < " << epsilon
 << "\nThe maximum number of iterations allowed is: " << imax << endl;
// determine the root
x0 = a;
f0 = f(x0);
dx0 = abs(b - a);
```

```cpp
// iterations
for (i = 1; i <= imax; i++)
{
x1 = x0 + dx0;
f1 = f(x1);
if (abs(f1) < epsilon) // root is found
{
cout << "\nRoot at x = " << x1 << " was found "
cout << "\nin " << i << " iterations" << endl;

cout << "\nThe value of the function is: " << f1 << endl;
return;
}
else // next iteration
dx1 = ( f1/(f0 - f1) ) * dx0;
x0 = x1;
dx0 = dx1;
f0 = f1;
}
```

```cpp
cout << "\nAfter " << imax << " iterations, no root was found "
 << "\nwithin the convergence criterion\n"
 << "The search for a root has failed due to excessive iterations\n"
 << "after the maximum number of: " << imax << " iterations" << endl;

return;
}
```

```cpp
// function to evaluate f(x)
double f(double x)
{
const double PI = 2*asin(1.0); // value of pi

return (exp(-x) - sin(0.5 * PI * x));
}
```

A sample run of Program 14.3 produced the following:

```
Enter the limits of the original search interval, a and b: .4 .5
Enter the convergence criteria: .00001
Enter the maximum number of iterations allowed: 25
```

The original search interval is from 0.4 to 0.5
The convergence criterion is: interval < 1e-005
The maximum number of iterations allowed is: 25

A root at x = 0.443628 was found in 4 iterations
The value of the function is -9.01417e-008

Although the secant method is probably the most popular method for finding the root of a function, it does pose divergence problems. For a reason, a check could be built into this method's C++ code detects that successive intervals start to become larger rather than smaller.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_792_0.png)

# EXERCISES 14.4

- 1. (Practice) Execute Program 14.3.
- 2. (Practice) Use Program 14.3 to find the root of the function f(x) = x^2 - 2x + 0.9, with an initial guess of x0 = 0.6 and x1 = 0.9.
- 3. (Practice) The secant ( ) function in Program 14.3 was used to find a root of the function f(x) = x^2 - 2x + 0.9. Starting with an initial guess of x0 = 0.6, x1 = 0.9, the values of x0 and x1 were displayed for each iteration as:

| Step | X0 | X1 - X0 |
|---|---|---|
| 0 | 0.600 | 0.300 |
| 1 | 0.900 | -0.180 |
| 2 | 0.720 | -0.057 |
| 3 | 0.663 | 0.022 |
| 4 | 0.685 | -0.001 |

Carefully graph the function for 0.5 ≤ x ≤ 1.0 and use the numbers in the preceding chart to show how the secant method arrives at a root of the function.
- 4. (Numerical) Use Program 14.3 to find a root of the function f(x) = x^2 - 2x - 3.

# 14.5 Introduction to Numerical Integration

The integration of a function of a single variable can be thought of as the opposite of differentiation—that is, the antiderivative—or as the area under a curve. Antiderivatives are ordinarily discussed in a calculus course. In this section, you concentrate instead on the less analytic, more visual approach of interpreting a definite integral as an area. The integral of the function $f(x)$ from $x=a$ to $x=b$, designated as

```
$I = \int_{a}^{b} f(x)dx$
```

will be evaluated by devising schemes for measuring the area under the graph of the function over this interval (see Figure 14.7). This method of evaluating an integral so naturally to numerical computation that the most effective way to understand the process of integration is to learn the numerical approach first and later have these ideas reinforced by more formal concepts of the antiderivative.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_793_0.png)

Another reason for studying numerical integration at this stage is that it's a stable process. It always works because numerical integration consists of expressing the area as the sum of smaller segments, a procedure fairly safe from problems such as division by zero or round-off error caused by subtracting numbers of the same magnitude. Finally it's unfortunately true that many, perhaps most, integrals occurring in actual engineering or science problems—obtaining a closed expression for the answer—takes considerable training and experience. Dozens of "tricks" must be learned. On the other hand, numerical integration procedures are few and all are easy to understand and remember. As in many other procedures, you begin by replacing the function over a limited range by straight segments. The interval $[a, b]$ is divided into subintervals of length $\Delta x$. The function is replaced by segments over each subinterval, and the area under the function is then approximated by the area under the line. This procedure is the trapezoidal approximation for an integral and is described in the next section. The next approximation is replacing the function by parabolic segments, known as Simpson's rule, and is explained in Section 14.7.

# 14.6 The Trapezoidal Rule

An approximation to the area under a curve is obtained by assuming the function can be replaced by simpler functions over a limited range. A straight line, the simplest approximation to a function, is to be considered first and called the trapezoidal rule. The area under the curve $f(x)$ from $x=a$ to $x=b$ is approximated by the area beneath a straight line drawn between the points $f(a)$ and $f(b)$ (see Figure 14.8). The area is then the approximation to the integral and the area of a trapezoid, which is the average value of $f$ times the width of interval:

$I \approx \frac{1}{2} [f(a) + f(b)](b - a) = T_0$

This is the trapezoidal rule for one panel, identified as $T_0$.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_794_0.png)

**Approximating the area under a curve by a single trapezoid**

To improve the accuracy of the approximation to the area under a curve, the interval is divided in half, and the function is approximated by straight-line segments over each half. Half the area in this example is approximated by the area of two trapezoids, as illustrated in Figure 14.9:

```
I = T_l = [\frac{\Delta x_l}{2}(f(a) + f_l)] + [\frac{\Delta x_r}{2}(f_l + f(b))] \quad \text{(incorrect in OCR)}
```

or

```
$T_l = \frac{\Delta x_l}{2}[f(a) + 2f_l + f(b)] \quad \text{(Equation 14.7)}$
```

where

```
$\Delta x_l = \frac{(b - a)}{2}$
```

$f_l = f(a + \Delta x_l)$

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_795_0.png)

**Figure 14.9 Two-panel approximation to the area**

Notice that when adding the areas of the trapezoids, the sides at $f(a)$ and $f(b)$ are sides of only the first and last trapezoid, while the side at $f_i$ is a side of two trapezoids, and therefore "counts twice", explaining the factor of 2 in Equation 14.7. Furthermore, the two-panel approximation, $T_2$, can be related to the one-panel results, $T_1$ as shown:

$T_2 = \frac{1}{2} T_1 + \Delta x f_i, \quad (\text{Equation 14.8})$

To increase the accuracy, the interval is simply subdivided into a large number of panels. The result for $n$ panels clearly clearly

$I = T_n = \frac{1}{2} f(a) + \sum_{i=1}^{n-1} f_i + \frac{1}{2} f(b) \quad (\text{Equation 14.9})$

where $\Delta x_n = (b-a)/n$, and $f_i$ is the function evaluated at each of the interior points: $f_i = f(a + i\Delta x_n)$

The reason for the extra factor of 2 in Equation 14.9 is the same as in the two-panel approximation. Equation 14.9 is known as the trapezoidal rule.

## Computational Form of the Trapezoidal Rule Equation

Equation 14.9 was derived assuming that the widths of all panels are the same and $\Delta x_n$. However, equal panels aren't required in the derivation, and the equation can be generalized easily to a partition of the interval into unequal panels of width $\Delta x_i, i = 1, \dots, n-1$. However, for reasons to be explained later, you'll restrict the width of the panel to be equal and the number of panels to a power of 2, as shown:

$n = 2^k$

The number of panels is $n$, the order of the calculation is called $k$ and the corresponding trapezoidal rule approximation is labeled $T_k$. $T_0$ is the result for $n=2^0=1$ panel. The situation for $k=2$ or $2^k=4$ panels is illustrated in Figure 14.10. In this figure, the width of a panel is $\Delta x_2 = (b-a)/2^2$, and the value of the $k=2$ trapezoidal rule approximation is following:

$T_2 = (\Delta x_2/2)[f(a) + 2f(a+\Delta x_2) + 2f(a+2\Delta x_2) + 2f(a+3\Delta x_2) + f(b)]$
