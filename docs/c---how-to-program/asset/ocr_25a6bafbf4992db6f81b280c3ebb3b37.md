# Good Programming Practice 21.1

Displaying bool values as true or false, rather than nonzero or 0, respectively, makes program outputs clearer.

```
```cpp
// Fig. 21.20: fig21_20.cpp
// Stream manipulators boolalpha and noboolalpha.
#include <iostream>
using namespace std;

int main()
{
    bool booleanValue = true;

    // display default true booleanValue
    cout << "booleanValue is " << booleanValue << endl;

    // display booleanValue after using boolalpha
    cout << "booleanValue (after using boolalpha) is "
         << boolalpha << booleanValue << endl << endl;

    cout << "switch booleanValue and use noboolalpha" << endl;
    booleanValue = false; // change booleanValue
    cout << noboolalpha << endl; // use noboolalpha

    // display default false booleanValue after using noboolalpha
    cout << "booleanValue is " << booleanValue << endl;

    // display booleanValue after using boolalpha again
    cout << "booleanValue (after using boolalpha) is "
         << boolalpha << booleanValue << endl;
} // end main
```
```

booleanValue is 1
booleanValue (after using boolalpha) is true

switch booleanValue and use noboolalpha

booleanValue is 0
booleanValue (after using boolalpha) is false

Fig. 21.20 | Stream manipulators boolalpha and noboolalpha.

# 21.7.8 Setting and Resetting the Format State via Member Function flags

Throughout Section 21.7, we've been using stream manipulators to change output format characteristics. We now discuss how to return an output stream's format to its default state after having applied several manipulations. Member function flags without an argument returns the current format settings as an fmtflags data type (of class ios_base), which represents the format state. Member function flags with an fmtflags argument sets the format state as specified by the argument and returns the prior state settings. The initial settings of the value that flags returns might differ across several systems. The program