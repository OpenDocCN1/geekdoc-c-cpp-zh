# 154 Assignment, Formatting, and Interactive Input

# Program 3.15

```
#include <iostream>
#include <iomanip>
#include <cmath>
using namespace std;

int main() {
    const double PI = 3.14159;
    const double DEG_TO_RAD = PI/180.0;
    double angle;

    cout << "Enter the angle (in degrees): ";
    cin >> angle;
    cout << setflags(ios::fixed)
         << setprecision(4)
         << "The sine of the angle is " << sin(angle * DEG_TO_RAD)
         << endl;

    return 0;
}
```

The following sample run was made using Program 3.15:

nEnter the angle (in degrees): 30
The sine of the angle is 0.5000

Although the const qualifier has been used to construct symbolic constants, you'll see this qualifier again in Chapter 6, where you'll learn it's useful as a function argument to make sure the argument isn't modified in the function.