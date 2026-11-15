# Modify!

These problems relate to the program developed in this section for computing velocity and acceleration values.

+   1. Enter different values of time until you find one that gives a velocity between 210 m/s and 211 m/s.
+   2. Enter different values of time until you find one that gives an acceleration between 0.5 m/s and 0.6 m/s.
+   3. Modify the program so that the input values are entered in minutes instead of seconds. Remember that the equations will still assume that the time values are in seconds.
+   4. Modify the program so that the output values are printed in feet per second, and feet per second². (Recall that 1 meter = 39.37 inches.)

# 2.9 System Limitations

In Section 2.2, we presented a table that contained the maximum values for the various types of integers and floating-point values for the Microsoft Visual C++ 6.0 compiler. To print a similar table for your system, use the program presented next. Note that the program includes three header files. The `iostream` header file is necessary because the program uses `cout`; the `climits` header file is necessary because it contains information relative to the ranges of integer types; and the `cfloat` header file is necessary because it contains information relative to the ranges of floating-point types. Appendix A contains more information on the constants and limits that are system dependent.

```
/*--------------------------------------------------------------*/
/* Program chapter2_7 */
/* */
/* This program prints the system limitations. */
/*--------------------------------------------------------------*/
#include<iostream>
#include<climits>
#include<cfloat>
using namespace std;
int main()
{
// Print integer type maxima. /
cout << "short maximum: " << sizeof(short) << endl;
cout << "int maximum: " << sizeof(int) << endl;
cout << "Long maximum: " << sizeof(long) << endl << endl;
```