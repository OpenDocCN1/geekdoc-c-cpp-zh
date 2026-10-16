
```
cout << "\n-->" << midPt << " is an approximate solution of " << " f(x) = 0, to within " << desiredAccuracy << endl;
}
```

```
// Function for which a root is being found
double f(double x)
{
    return x*x*x + x - 5;
}
```

## SAMPLE RUN:

This program uses the bisection method to find an approximate solution to the equation f(x) = 0.

Enter the accuracy desired (e.g. .001): 1e-4
Enter endpoints of an interval containing a solution: 0 1
Enter endpoints of an interval containing a solution: 0 2

-->1.51599 is an approximate solution of f(x) = 0, to within 0.0001

## 6.5.2 Numerical Integration—Approximating Areas of Regions

One important problem in calculus is finding the area of a region bounded below by the x-axis, above by the graph of a function y = f(x), on the left by a vertical line x = a, and on the right by a vertical line x = b:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_195_0.png)

More generally, the problem is to approximate the integral

∫ₐᵇ f(x) dx

One common method is to divide the interval [a, b] into n subintervals, each of width Δx = (b − a)/n using n − 1 equally spaced points x₁, x₂, ..., xₙ₋₁. Locating the corresponding points on the curve and connecting consecutive points using line segments forms n trapezoids:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_196_0.png)

The sum of the areas of these trapezoids is approximately the area under the graph of f; thus, this method is known as the trapezoidal method for approximating integrals. (The programming problems describe Simpson's method, which uses parabolas instead of trapezoids.) The formula for the area of a trapezoid gives

> \frac{1}{2} \Delta x (y_{i-1} + y_i)

for the area of the ith trapezoid, where y_{i-1} and y_i are the values of the function f at x_{i-1} and x_i, respectively. Summing these and combining terms gives the formula

> \Delta x \left( \frac{y_0 + y_n}{2} + y_1 + y_2 + \cdots + y_{n-1} \right)

or written more concisely using summation (Σ) notation,

> \Delta x \left( \frac{y_0 + y_n}{2} + \sum_{i=1}^{n-1} y_i \right)

The program in Example 6.12 implements the trapezoidal method.

## Example 6.12 Trapezoidal Approximation of an Integral

```
/* This program approximates the area under the graph of a function
f() over an interval [a, b] using the trapezoidal rule -- and
thus approximates the definite integral of f() from a to b.

Input: the endpoints a and b of the interval, and the number of
subintervals to use

Output: approximation to the integral of f() on [a, b] */
```

```
#include <iostream>      // cin, cout, <<, >>
using namespace std;

double f(double x);      // function to be integrated

int main()
{
    cout << "Trapezoidal approximation of an integral:\n";

    int n;                  // number of subintervals
    double a, b,            // endpoints of interval
           deltaX,          // length of subintervals
           x, y,            // point on graph of f()
           sum;             // sum of areas of trapezoids

    cout << "Enter interval endpoints and the # of subintervals: ";
    cin >> a >> b >> n;

    deltaX = (b - a) / n;
    sum = 0;
    x = a;

    for (int i = 1; i <= n - 1; i++)
    {
        x += deltaX;
        y = f(x);
        sum += y;
    }
    sum = deltaX * ((f(a) + f(b))/2 + sum);

    cout << "Approximate value using " << n << " subintervals: "
         << sum << endl;
}

// Function being integrated
double f(double x)
{ return x*x + .1; }
```

## SAMPLE RUNS:

Trapezoidal approximation of an integral:
Enter interval endpoints and the # of subintervals: 0 1 10
Approximate value using 10 subintervals: 1.335

Trapezoidal approximation of an integral:
Enter interval endpoints and the # of subintervals: 0 1 50
Approximate value using 50 subintervals: 1.3334

Trapezoidal approximation of an integral:

that satisfies a given initial condition:

y(x₀) = y

Euler’s method for obtaining an approximate solution over some interval [a, b], where a = x₀, is as follows:

- 1. Select an x-increment Δx.
- 2. For n = 0, 1, 2, …, do the following:
- a. Set xₙ₊₁ = xₙ + Δx.
- b. Find the point Pₙ₊₁(xₙ₊₁, yₙ₊₁) on the line through Pₙ(xₙ, yₙ) with slope f(xₙ, yₙ).
- c. Output yₙ₊₁, which is the approximate value of y at xₙ₊₁.

The following diagram illustrates Euler’s method:

![](img/ee01f74bfb7397ce74bbc4286ed2dd55_199_0.png)

The program in Example 6.13 uses Euler’s method to find an approximate solution for

y' = 2xy

y(0) = 1

Sample runs with a = 0, b = 1, Δx = 0.2 and a = 0, b = 0.5, Δx = 0.05 are shown.

## Example 6.13 Euler’s Method for Solving a Differential Equation

```
/* This program uses Euler's method to obtain an approximate solution
to a first-order differential equation of the form y' = f(x, y)

Input:  initial values for x and y, an increment deltaX, and
        number of iterations
```

Output: a sequence of points (x, y) that approximate the solution curve

```
#include <iostream>      // cin, cout, <<, >>
#include <iomanip>      // output formatters
using namespace std;

double f(double x, double y);

int main()
{
    cout << "Euler's method for solving a differential equation:\n";

    double x, y,            // current x value, y value
           xNext, yNext,    // next x value, y value
           deltaX;          // x-increment used
    int numIterations;      // number of iterations.

    cout << "Enter x0 and y0, x-increment to use, and "
         << "number of values to calculate:\n";
    cin >> x >> y >> deltaX >> numIterations;

    cout << "  X              Y\n"
         << "========================\n"
         << fixed << setprecision(5) << showpoint
         << setw(10) << x << setw(10) << y << endl;

    // Iterate with Euler's method

    for (int n = 1; n <= numIterations; n++)
    {
        xNext = x + deltaX;
        y = y + f(x, y) * deltaX;
        x = xNext;
        cout << setw(10) << x << setw(10) << y << endl;
    }
}

double f(double x, double y)
{ return 2.0 * x * y; }
```

## SAMPLE RUNS:

Euler's method for solving a differential equation:
Enter x0 and y0, x-increment to use, and number of values to calculate:
0 1 0.2 5

## 186 ■ Programming in C++ for Engineering and Science

| X | Y |
| --- | --- |
| 0.00000 | 1.00000 |
| 0.20000 | 1.00000 |
| 0.40000 | 1.08000 |
| 0.60000 | 1.25280 |
| 0.80000 | 1.55347 |
| 1.00000 | 2.05058 |

Euler's method for solving a differential equation:

Enter x0 and y0, x-increment to use, and number of values to calculate:

0 1 .05 10

| X | Y |
| --- | --- |
| 0.00000 | 1.00000 |
| 0.05000 | 1.00000 |
| 0.10000 | 1.00500 |
| 0.15000 | 1.01505 |
| 0.20000 | 1.03028 |
| 0.25000 | 1.05088 |
| 0.30000 | 1.07715 |
| 0.35000 | 1.10947 |
| 0.40000 | 1.14830 |
| 0.45000 | 1.19423 |
| 0.50000 | 1.24797 |

- | Term | Corresponding |
|------|-------------|
| #include directive | function |
| abstraction | function declaration |
| argument | function definition |
| body of a function | function heading |
| call to a function | function prototype |
| compilation | function stub |
| documentation file | header file |
| driver program | implementation file |
| encapsulation | information hiding |
| executable program | interface file |
| executable file | library |

- A function's documentation should include its *specification*—descriptions of its parameters and their types, values input to the function, what it returns, values it outputs, preconditions, and postconditions.
- Local variables, constants, and parameters exist only while a function is executing and thus can be accessed only within the function. This means that other functions may reuse the name of a local item for some other purpose without causing a conflict.
- A library is a collection of files:
  - A *header file* that contains declarations and prototypes of a library's items that is also called the *interface file* because it acts as an interface between the library and client programs. It is inserted into a program (or another library) using a directive of the form `#include "Library.h"`.
  - An *implementation file* that contains definitions of items not defined in the header file. It must be separately compiled and then linked to a client program. Items defined in it that are declared in the header file can be accessed in any program that `#includes` the header file and links to this implementation file. Items defined here but not declared in the header file cannot be accessed outside of this implementation file, even by a program that `#includes` the header file.
  - A *documentation file* that contains documentation for the library's items.

## Style and Design Tips

- *Functions should be documented in the same way as programs.* The documentation should include the following:
  - A statement of what it does
  - Its specification, which consists of those of the following that apply:
    - what it receives (i.e., its parameters);
    - what is input to the function;
    - preconditions—restrictions or limitations on the parameters' values in order for the function to work properly;
    - what it returns;
    - what it outputs;
    - postconditions—effects produced by the function.

In this text, to avoid cluttering the header and implementation files, we place the documentation for functions stored in a library in a separate documentation file.

- *Functions are separate program components, and the white space in a program should reflect this.* In this text, we
