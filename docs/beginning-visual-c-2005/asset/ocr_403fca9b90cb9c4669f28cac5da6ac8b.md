It should be clear from what you have seen up to now that when a derived class constructor is executed, a base class constructor is always called to construct the base part of the derived class object. If you don’t specify the base class constructor to be used, the compiler arranges for the default base class constructor to be called.

The last line in the table shows that the initialization of the base part of the myMintBox object is working as it should be, with the private members having been initialized by the CBox class constructor.

Having the private members of a base class only accessible to function members of the base class isn’t always convenient. There will be many instances where you want to have private members of a base class that can be accessed from within the derived class. As you surely have anticipated by now, C++ provides a way to do this.

# Declaring Class Members to be Protected

In addition to the public and private access specifiers for members of a class, you can also declare members of a class as protected. Within the class, the protected keyword has the same effect as the private keyword: members of a class that are protected can only be accessed by member functions of the class, and by friend functions of the class (also by member functions of a class that is declared as a friend of the class — you will learn about friend classes later in this chapter). Using the protected keyword, you could redefine the CBox class as follows:

```
// Box.h in Ex9_04
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox
{
public:
    // Base class constructor
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0):
        m_Length(lv), m_Width(wv), m_Height(hv)
    { cout << endl << "CBox constructor called"; }
```

```
// CBox destructor - just to track calls
~CBox()
{ cout << "CBox destructor called" << endl; }
```

```
protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

Now the data members are still effectively private, in that they can’t be accessed by ordinary global functions, but they’ll still be accessible to member functions of a derived class.