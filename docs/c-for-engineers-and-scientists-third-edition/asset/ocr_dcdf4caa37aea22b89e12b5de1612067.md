# Program 6.15

```
#include <iostream>
using namespace std;

int firstnum; // create a global variable named firstnum

void valfun(); // function prototype (declaration)

int main() {
    int secnum; // create a local variable named secnum
    firstnum = 10; // store a value in the global variable
    secnum = 20; // store a value in the local variable

    cout << "From main(): firstnum = " << firstnum << endl;
    cout << "From main(): secnum = " << secnum << endl;

    valfun(); // call the function valfun

    cout << "\nFrom main() again: firstnum = " << firstnum << endl;
    cout << "From main() again: secnum = " << secnum << endl;
    return 0;
}

void valfun() {\ // no values are passed to this function
    int secnum; // create a local variable named secnum
    secnum = 30; // affects only this local variable's value

    cout << "\nFrom valfun(): firstnum = " << firstnum << endl;
    cout << "From valfun(): secnum = " << secnum << endl;

    firstnum = 40; // changes firstnum for both functions

    return;
}
```