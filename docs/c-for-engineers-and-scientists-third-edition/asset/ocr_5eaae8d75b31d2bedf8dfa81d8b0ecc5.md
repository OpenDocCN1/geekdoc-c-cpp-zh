# Assignment, Formatting, and Interactive Input

# Program 3.14

```
// This program determines the weight of a steel cylinder
// by multiplying the volume of the cylinder its density.
// The volume of the cylinder is given by the formula PI * pow(radius,2) * height.
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

int main() {
    const double PI = 3.1416;
    const double DENSITY = 0.284;
    double radius, height;

    cout << "The radius of the cylinder (in inches): " <<;
    cin >> radius;
    cout << "The height of the cylinder (in inches): " <<;
    cin >> height;
    weight = DENSITY * PI * pow(radius,2) * height;
    cout << setios(ios::fixed)
         << setflags(ios::showpoint)
         << setprecision(4)
         << "The cylinder weighs " << weight << " pounds" << endl;

    return 0;
}

```

Notice in Program 3.14 two symbolic constants have been defined: PI and DENSITY. The following run was made to determine the weight of the cylinder with a radius of 3 inches and a height of 12 inches.

Enter the radius of the cylinder (in inches): 3
Enter the height of the cylinder (in inches): 12
The cylinder weighs 96.3592 pounds

The advantage of using the named constant PI in Program 3.14 is that it clearly identifies the value of 3.1416 in terms most people recognize. The advantage of using the named constant DENSITY is that the programmer can change the value of the density for another material without having to search through the program to where DENSITY is used. If, course, many different materials are used, DENSITY should be changed from a symbolic constant to a variable. A natural question, then, is asking the difference between symbolic constants and variables.