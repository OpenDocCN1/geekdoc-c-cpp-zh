This prototype and function header are included in Program 6.8, which uses a newval() function body that displays and alters the values stored in these reference variables from within the called function.

# Program 6.8

```
#include <iostream>
using namespace std;

void newval(double&, double&);  // prototype with two reference parameters

int main()
{
    double firstnum, secnum;

    cout << "Enter two numbers: ";
    cin >> firstnum >> secnum;
    cout << "\nThe value in firstnum is: " << firstnum << endl;
    cout << "The value in secnum is: " << secnum << "\n\n";

    newval(firstnum, secnum);    // call the function

    cout << "The value in firstnum is now: " << firstnum << endl;
    cout << "The value in secnum is now: " << secnum << endl;

    return 0;
}

void newval(double& xnum, double& ynum)
{
    cout << "The value in xnum is: " << xnum << endl;
    cout << "The value in ynum is: " << ynum << "\n\n";
    xnum = 89.5;
    ynum = 99.5;

    return;
}
```

In calling the newval() function in Program 6.8, you need to understand the connection between the arguments used in the function call, firstnum and secnum, and the parameters used in the function header, xnum and ynum. Both refer to the same data items. The significance is that the values in the arguments (firstnum and secnum) can now be altered from within newval() by using the parameter names (xnum and ynum). Therefore, the parameters