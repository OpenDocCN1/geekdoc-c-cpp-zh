# Chapter 15 Friends, Exceptions, and More

```
class bad_gmean
{
public:
    double v1;
    double v2;
    bad_gmean(double a = 0, double b = 0) : v1(a), v2(b){}
    const char * mesg();
};
```

```
inline const char * bad_gmean::mesg()
{
    return "gmean() arguments are >=\n";
}
```

# Listing 15.11 error4.cpp

```
//error4.cpp - using exception classes
#include <iostream>
#include <cmath> // math.h, unix users may need -lm flag
#include "exc_gmean.h"
// function prototypes
double hmean(double a, double b);
double gmean(double a, double b);
int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

    double x, y, z;

    cout << "Enter two numbers: ";
    while (cin >> x >> y)
    {
        try {
            z = hmean(x,y);
            cout << "Harmonic mean of " << x << " and " << y << "\n";
            cout << " is " << z << endl;
            cout << "Geometric mean of " << x << " and " << y << "\n";
            cout << " is " << gmean(x,y) << endl;
            cout << "Enter next set of numbers <q to quit>: ";
        }
        catch (bad_gmean & bg)
        {
            bg.mesg();
            cout << "Try again.\n";
        }
    }
```