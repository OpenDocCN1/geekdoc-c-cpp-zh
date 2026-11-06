This line of code creates a type called `FullPtr`, which is a pointer to a function that takes a `FullOvenManip` parameter and returns a void. We can think of only one function that does that! It’s the `FullOvenInfo()` function. Woo-hoo!

![](bbox=[0.13, 0.2, 0.21, 0.28])

When writing your own manipulators, don’t shy away from using `typedef`. The manipulator concept is confusing, and can be a serious struggle for many of us to keep straight. By using a `typedef`, you can simplify your life a bit.

Here’s the overloaded `operator >>` function header:

```
ostream &operator << (ostream &out, FullPtr);
```

You can see the second parameter: It’s a `FullPtr`. And look at this code:

```
cout << FullOvenInfo;
```

The `FullOvenInfo` item is also a `FullPtr` because it’s a pointer to a function that takes a `FullOvenManip()` value. That does the trick.

The `CustomManipulator` example in Listing 5-1 is a really great example of all this!

# Listing 5-1: Using Manipulators

```
#include <iostream>
#include <string>
#include <fstream>
#include <map>

using namespace std;

class MicrowaveOven
{
    friend ostream &operator << (ostream &out,
        MicrowaveOven &oven);
public:
    typedef map<ostream *, bool> FlagMap;
    int HighVoltageRadiation;
    int RadioactiveFoodCount;
    int LeakLevel;
    string OvenName;
    static FlagMap Flags;
};

MicrowaveOven::FlagMap MicrowaveOven::Flags;
ostream &operator << (ostream &out, MicrowaveOven &oven)
{
    bool full = true;
    MicrowaveOven::FlagMap::iterator iter =
        MicrowaveOven::Flags.find(&out);
    if (iter != MicrowaveOven::Flags.end())
    {
        full = iter->second;
    }
}
```