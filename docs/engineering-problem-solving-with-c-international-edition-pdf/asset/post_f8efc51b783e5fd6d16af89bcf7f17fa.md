
![](img/f2bfa570e453b020c16e048c79a3ea0e_310_0.png)

### Figure 6.14 Area under a curve.

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_1.png)

### Figure 6.15 Spaced intervals.

If we join the points on the curve with straight-line segments, we form a group of trapezoids whose combined areas approximate the area under the curve. The closer the points are together on the curve, the more trapezoids there are in the interval, and thus the more accurate will be our approximation to the integral. In Figure 6.16, we use five points on the curve to generate four trapezoids, and the sum of the areas of the four trapezoids is then an approximation to the integral of the function between a and b.

The area of a trapezoid is one-half times the base times the sum of the two heights (or sides):

Area = 1/2 * base * (height₁ + height₂).

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_2.png)

![](img/f2bfa570e453b020c16e048c79a3ea0e_310_3.png)

### Figure 6.16 Four trapezoids.

Thus, the area of the first trapezoid, $A_1$, is computed using the pair of points $(x_1, y_1)$ and $(x_2, y_2)$:

$A_1 = 1/2 * (x_2 - x_1) * (y_1 + y_2)$.

Since the points on the curve are equally spaced along the x-axis in this example, the base of each of the trapezoids is the same value. We can then compute the individual areas of the trapezoids as

- A1 = 1/2 * base * ($y_1$ + $y_2$),
- A2 = 1/2 * base * ($y_2$ + $y_3$),
- A3 = 1/2 * base * ($y_3$ + $y_4$),
- A4 = 1/2 * base * ($y_4$ + $y_5$).

Thus, the total area between $a$ and $b$ can be approximated by the sum of the areas of the four trapezoids:

$$\int_a^b f(x) dx \approx \frac{base}{2} ((y_1 + y_2) + (y_2 + y_3) + (y_3 + y_4) + (y_4 + y_5))$$
$$\approx \frac{base}{2} (y_1 + 2y_2 + 2y_3 + 2y_4 + y_5).$$

In general, if the area under a curve is divided into $N$ trapezoids with equal bases, the area can be approximated by the following equation:

$$\int_a^b f(x) dx \approx \frac{base}{2} \left( y_1 + 2 \sum_{k=2}^N y_k + y_{N+1} \right).$$

This equation is referred to as the trapezoidal rule.

When computing an integral with this numerical technique, we need to remember that the data points on the curve could come from different sources. If we have the equation for the curve, a C++ program can compute the data points that we use as the height of the trapezoids; in this case, we can choose the data points to be as close together or as far apart as we wish. Another possibility is that the points are experimentally collected data; in this case, we have a set of x-coordinates that represent the trapezoid base values and the y-coordinates that represent the heights of the trapezoids. We can still use the trapezoid areas to estimate the integral, but we cannot choose data points that are closer together or farther apart, because we do not have a function to evaluate; we only have the available data to use. If the bases of the trapezoids determined by the data points are not of equal value, we have to add the areas of the trapezoids individually instead of using the equation that assumes that the bases are equal.

We will now present a C++ program that determines an estimate of the integral (between two specified points) of the following equation:

$y = f(x)$
$= 4e^{-x}.$

```cpp
/*-------------------------------- Program chapter6_12 ----------------------------------*/
/*                                                                                       */
/*   Program chapter6_12                                                                 */
/*                                                                                       */
/*   This program estimates the area under a given curve                                 */
/*   using trapezoids with equal bases.                                                  */
/*---------------------------------------------------------------------------------------*/
#include<iostream>    //Required for cin, cout
#include<cmath>       //Required for exp()
using namespace std;

// Function prototypes.
double integrate(double a, double b, int n);
double f(double x);

int main()
{
   // Declare objects
   int num_trapezoids;
   double a, b, area;

   // Get input from user.
   cout << "Enter the interval endpoints, a and b\n";
   cin >> a >> b;
   cout << "Enter the number of trapezoids\n";
   cin >> num_trapezoids;

   // Estimate area under the curve of 4e^-x
   area = integrate(a, b, num_trapezoids);

   // Print result.
   cout << "Using " << num_trapezoids
        << " trapezoids, the estimated area is "
        << area << endl;

   return 0;
}
```

```cpp
double integrate(double a, double b, int n)
{
   // Declare objects.
   double sum(0), x, base, area;

   base = (b-a)/n;
   for(int k=2; k<=n; k++)
   {
      x = a + base*(k-1);
      sum = sum + f(x);
   }
   area = 0.5*base*(f(a) + 2*sum + f(b));
   return area;
}
```

```cpp
double f(double x)
{
    return(4*exp(-x));
}
/*-------------------------------------------------------------*/
```

The following are some sample runs of the preceding program:

```
Enter the interval endpoints, a and b
0
1
Enter the number of trapezoids
5
Using 5 trapezoids, the estimated area is 2.536905
--------------------------------------------------------------
Enter the interval endpoints, a and b
0
1
Enter the number of trapezoids
50
Using 50 trapezoids, the estimated area is 2.528567
--------------------------------------------------------------
Enter the interval endpoints, a and b
0
1
Enter the number of trapezoids
100
Using 100 trapezoids, the estimated area is 2.528503
```

If we use calculus to integrate the specified function over the interval [0, 1], the theoretical answer to seven digits of accuracy is 2.528482.

## SUMMARY

Most programs in C++ benefit from using both library and programmer-defined functions. Functions allow us to reuse software and to employ abstraction in our solution, and, hence, reduce development time and increase the quality of the software. Numerous examples were developed to illustrate using value returning programmer-defined functions to solve problems, including examples of recursive functions. Specific applications were presented to illustrate generating random numbers (integers or floating-point values) and to implement the incremental search technique and Newton-Raphson method for identifying real roots of polynomials as well as numerical integration using the trapezoidal rule.

## Key Terms

| abstraction | computer simulation |
|---|---|
| accessor methods | custom header file |
| address operator | encapsulation |
| automatic storage class | external storage class |
| center of gravity | function argument |
| coercion of arguments | formal parameter |
| composite materials | function |

- function argument
- function body
- function header
- function prototype
- global scope
- incremental search
- library function
- local scope
- modularity
- module
- module chart
- moment
- mutator methods
- Newton-Raphson method
- numerical integration
- parameter declarations
- pass by reference
- pass by value
- public interface
- programmer-defined function
- random number
- random number seed
- register class
- reliability
- re-usability
- root
- scope
- simulation
- stable system
- static storage class
- storage class
- structure chart
- system
- trapezoidal rule

## C++ Statement Summary

### Function definition:

```
return_type function_name(parameter types)
{
    declarations:
    statements:
}
```

### Method definition:

```
return_type class_name::function_name(parameter types)
{
    declarations:
    statements:
}
```

### Return statements:

void function:

```
return;
```

### Value returning function:

```
return ( a + b)/2;
```

### Function prototype:

```
double sinc(double x);
double sinc(double);
void check_roots(double left, double right, double a0,
                 double a1, double a2, double a3);
```
