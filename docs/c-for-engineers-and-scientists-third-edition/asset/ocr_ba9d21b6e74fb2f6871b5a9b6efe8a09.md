# Chapter 6 337

A Case Study: Rectangular to Polar Coordinate Conversion

# Program 6.11

```
#include <iostream>
#include <cmath>
using namespace std;

void polar(double, double, double&); // function prototype

int main()
{
    double distance, angle;
    polar(3.0, 4.0, distance, angle);

    cout << "r = " << distance << endl;
    cout << "angle = " << angle << endl;

    return 0;
}

void polar(double x, double y, double& r, double& theta)
{
    const double DEGREES = 180.0/3.141593;

    r = sqrt(x * x + y * y);
    theta = atan(y/x) * DEGREES;

    return;
}
```

Notice that in main(), the literals 3.0 and 4.0 are passed to polar(). The function accepts these inputs as the parameters x and y and uses these parameters in calculating values for the parameters r and theta. In main(), these last two parameters are known as distance and angle, and their values are displayed immediately after the call to polar() is made. This is the output produced When Program 6.11 runs:

r = 5
angle = 53.1301

These results are the same as those you would get from a hand calculation. As the function performs only two calculations, and the results displayed by the test program agree with those from a hand calculation, the function has been completely tested. It still remains to group tested with the other two functions required for the complete program to make sure correct argument values are exchanged between each function.