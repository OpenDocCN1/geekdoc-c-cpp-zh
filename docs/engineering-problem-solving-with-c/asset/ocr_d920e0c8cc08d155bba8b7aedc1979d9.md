we cannot choose data points that are closer together or farther apart, because we do not have a function to evaluate; we only have the available data to use. If the bases of the trapezoids determined by the data points are not of equal value, we have to add the areas of the trapezoids individually instead of using the equation that assumes that the bases are equal.

We will now present a C++ program that determines an estimate of the integral (between two specified points) of the following equation:

y = f(x)
= 4e⁻ˣ.

```
/*--------------------------------------------------------------*
/* Program chapter6_12                                          */
/*                                                              */
/* This program estimates the area under a given curve          */
/* using trapezoids with equal bases.                           */
/*--------------------------------------------------------------*/

#include<iostream> //Required for cin, cout
#include<cmath> //Required for exp()
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

 // Estimate area under the curve of 4e⁻ˣ
 area = integrate(a, b, num_trapezoids);

 // Print result.
 cout << "Using " << num_trapezoids
 << " trapezoids, the estimated area is "
 << area << endl;

 return 0;
}
/*--------------------------------------------------------------*/
```