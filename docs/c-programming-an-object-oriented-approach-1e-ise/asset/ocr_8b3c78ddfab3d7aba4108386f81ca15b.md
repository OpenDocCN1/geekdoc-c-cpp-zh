```
```cpp
// Return-by-value                                      // Return-by-reference
int larger (int x, int y)                              int& larger (int& x, int& y)
{                                                     {
    if (x > y)                                            if (x > y)
    {                                                     {
        return x;                                            return x;
    }                                                     }
    return y;                                              return y;
}                                                     }
int main ()                                            int main ()
{                                                     {
    int x = 10;                                             int x = 10;
    int y = 20;                                             int y = 20;
    int z = larger (x, y);                                  int z = larger (x, y);
    cout << z;                                              cout << z;
    return 0;                                               return 0;
}                                                     }

Run:                                                  Run:
20                                                    20
```
```

We see examples of both practices in cases like this because the cost of copying is small in pass-by-value and return-by-value.

# EXAMPLE 9.10

In this example we find the larger between two objects of class types. In Chapter 7 we created a fraction class. We do not repeat the interface and the implementation file here (separate compilation). We just create an application file that uses pass-by-reference and return-by-reference to find the smaller of two fractions. Program 9.3 shows the application file.

# **Program 9.3**  Finding the larger of two fractions

```
```cpp
/***************************************************************
 * The program creates two pairs of fractions and then calls a  *
 * function named larger to find the larger in each pair        *
 ***************************************************************/
#include "fraction.h"

Fraction& larger (Fraction&, Fraction&);  // Prototype

int main ( )
{
    // Creating first pair of fractions and finding the larger
    Fraction fract1 (3, 13);
    Fraction fract2 (5, 17);
    cout << "Larger of the first pair of fraction: ";
    larger (fract1, fract2).print ();
    // Creating second pair of fractions and finding the larger
```
```