# DISPLAY 14.3 The Recursive Function power

```
//Program to demonstrate the recursive function power.
#include <iostream>
#include <cstdlib>
using namespace std;

int power(int x, int n);
//Precondition: n >= 0.
//Returns x to the power n.

int main()
{
    for (int n = 0; n < 4; n++)
        cout << "3 to the power " << n
            << " is " << power(3, n) << endl;
    return 0;
}

//uses iostream and cstdlib:
int power(int x, int n)
{
    if (n < 0)
    {
        cout << "Illegal argument to power.\n";
        exit(1);
    }
    if (n > 0)
        return ( power(x, n - 1) * x);
    else // n == 0
        return (1);
}
```

# Sample Dialogue

```
3 to the power 0 is 1
3 to the power 1 is 3
3 to the power 2 is 9
3 to the power 3 is 27
```

Our main reason for defining the function power is to have a simple example of a recursive function, but there are situations in which the function power would be preferable to the function pow. The function pow returns values of type double, which are only approximate quantities. The function power returns values of type int, which are exact quantities. In some situations, you might need the additional accuracy provided by the function power.