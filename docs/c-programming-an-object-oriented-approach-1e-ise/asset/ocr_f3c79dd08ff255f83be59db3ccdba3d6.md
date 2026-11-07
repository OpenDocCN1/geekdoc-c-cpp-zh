+   a. If the value of the term is negative, there are no real roots (they are complex).
+   b. If the value of the term is zero, the two roots are the same and the common value is −b/2a.
+   c. If the value of the term is positive, the two roots are distinct and their values are −b + (b² − 4ac)¹ᐟ² and −b − (b² − 4ac)¹ᐟ².

We can use these three facts to find the roots of any quadratic expression, as shown in Program 6.2.

# Program 6.2  Calculating the root of a quadratic equation

```
/************************************************************
 * This program finds the roots of the quadratic equations  *
 ************************************************************/
#include <iostream>
#include <cmath>
using namespace std;

int main ( )
{
    // Declaration of variables
    int a, b, c;
    double term;
    // Inputting the value of three coefficients
    cout << "Enter the value of coefficient a: ";
    cin >> a;
    cout << "Enter the value of coefficient b: ";
    cin >> b;
    cout << "Enter the value of coefficient c: ";
    cin >> c;
    // Calculating the value of term (b² − 4ac)
    term = pow (b, 2) − 4 * a * c;
    if (term < 0)
    {
        cout << "There is no root!" << endl;
    }
    else if (term == 0)
    {
        cout << "The two roots are equal." << endl;
        cout << "x1 = x2 = " << −b / (2 * a) << endl;
    }
    else
    {
        cout << "There are two distinct roots:" << endl;
        cout << "x1 = " << (−b + sqrt (term)) / (2 * a) << endl;
        cout << "x2 = " << (−b − sqrt (term)) / (2 * a) << endl;
```