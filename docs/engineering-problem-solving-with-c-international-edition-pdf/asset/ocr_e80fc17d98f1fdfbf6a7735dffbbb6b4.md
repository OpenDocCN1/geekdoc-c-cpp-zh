```
else
    if f_left * f_right < 0
        return print root at midpoint of subinterval
poly(x,a0,a1,a2,a3);
    return a0*x^3 + a1x^2 + a2x + a3
```

Note in the pseudocode for the check_root() function that we check to see whether the left subinterval endpoint is a root, but we do not check the right subinterval endpoint. This is necessary to avoid identifying the same root twice: when it is a right endpoint for one interval and also when it is a left endpoint for the next subinterval. Because we only check the left endpoints, we need to check the final point in the interval because it never becomes a left endpoint.

The steps in the pseudocode are detailed enough to convert to C++:

```
//*****************************************************************
//  Program chapter6_10
//*
//  This program estimates the real roots of a
//  polynomial function using incremental search.    */
#include<iostream>   //Required for cin, cout
#include<cmath>      //Required for cell()
using namespace std;
// Function Prototypes
void check_roots(double left, double right, double a0,
                 double a1, double a2, double a3);
double poly(double x, double a0, double a1,
            double a2, double a3);
int main()
{
   // Declare objects and function prototypes.
   int n;
   double a0, a1, a2, a3, a, b, step, left, right;
   // Get user input.
   cout << "Enter coefficients a0, a1, a2, a3: \n";
   cin >> a0 >> a1 >> a2 >> a3;
   cout << "Enter interval limits a, b (a<b): \n";
   cin >> a >> b;
   cout << "Enter step size: \n";
   cin >> step;
   //Check subintervals for roots.
   n = ceil((b - a)/step);
   for (int k=0; k<=n-1; k++)
   {
      left = a + k*step;
      if (k == n-1)
          right = b;
```