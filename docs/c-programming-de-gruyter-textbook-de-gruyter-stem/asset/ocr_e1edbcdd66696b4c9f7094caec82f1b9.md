# 82 — 3 Functions

Source code:

```
//3_2.cpp
#include <iostream>
using namespace std;
double power (double x, int n);

int main()
{
    int i;
    int value = 0;
    char ch;

    cout << "Enter an 8 bit binary number ";
    for (i = 7; i >= 0; i--)
{
        cin >> ch;
        if (ch == '1')
            value += int(power(2,i));
    }
    cout <<"Decimal value is "<<value<<endl;\n}

double power (double x, int n)
{
    double val = 1.0;
    while (n--)
        val *= x;
    return(val);
}
```

Running result:

| Enter an 8 bit binary number 01101001 |
| Decimal value is 105 |

**Example 3.3:** Write a program to compute the value of $\pi$ using the following formula.

$\pi = 16 \arctan\left(\frac{1}{5}\right) - 4 \arctan\left(\frac{1}{239}\right)$

Use the following series to calculate the arctangent of a number: