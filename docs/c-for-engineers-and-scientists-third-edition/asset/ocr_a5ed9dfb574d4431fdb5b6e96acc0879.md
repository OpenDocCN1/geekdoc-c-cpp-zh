# Program 6.12

```
#include <iostream>
using namespace std;

void getrec(double&, double&); // function prototype

int main() {
    double xcoord, ycoord;

    getrec(xcoord, ycoord);

    cout << "The entered value for x is " << xcoord << endl;
    cout << "The entered value for y is " << ycoord << endl;

    return 0;
}

void getrec(double& x, double& y) {
    cout << "Rectangular to Polar Coordinate\n" Conversion Program\n" << endl;
    cout << "Enter the x coordinate: ";
    cin >> x;
    cout << "Enter the y coordinate: ";
    cin >> y;
    return;
}
```

The function for displaying polar coordinates is constructed in a similar manner. Program 6.13 contains both the function, named showit(), and a front-end driver for testing the function. Notice that the parameter names in the function header for showit() need not be the same as those used in any other function. showit() is constructed to simply display the values in its two parameters, which in this case have named radius and angle.
The following output of Program 6.13 verifies that showit() displays the values passed to it correctly:

The polar coordinates are:
Distance from origin: 5
Angle (in degrees) from x-axis: 53.1301