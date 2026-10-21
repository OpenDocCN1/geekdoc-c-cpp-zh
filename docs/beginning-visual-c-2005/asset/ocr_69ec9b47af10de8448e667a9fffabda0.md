You should not conclude, from the previous example of the CContainer class, that an abstract class can’t have data members. An abstract class can have both data members and function members. The presence of a pure virtual function is the only condition that determines that a given class is abstract. In the same vein, an abstract class can have more than one pure virtual function. In this case, a derived class must have definitions for every pure virtual function in its base; otherwise, it too will be an abstract class. If you forget to make the derived class version of the Volume() function const, the derived class will still be abstract because it contains the pure virtual Volume() member function that is const, as well as the non-const Volume() function that you have defined.

# Try It Out
An Abstract Class

You could implement a CCan class, representing beer or cola cans perhaps, together with the original CBox class and derive both are derived from the CContainer class that you defined in the previous section.. The definition of the CBox class as a subclass of CContainer is as follows:

```
// Box.h for Ex9_10
#pragma once
#include "Container.h"      // For CContainer definition
#include <iostream>
using std::cout;
using std::endl;

class CBox: public CContainer      // Derived class
{
public:

    // Function to show the volume of an object
    virtual void ShowVolume() const
    {
        cout << endl
             << "CBox usable volume is " << Volume();
    }

    // Function to calculate the volume of a CBox object
    virtual double Volume() const
    { return m_Length*m_Width*m_Height; }

    // Constructor
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
        :m_Length(lv), m_Width(wv), m_Height(hv) {}

protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

The unshaded lines are the same as in the previous version of the CBox class. The CBox class is essentially as we had it in the previous example, except this time you have specified that it is derived from the CContainer class. The Volume() function is fully defined within this class (as it must be if this class is to be used to define objects). The only other option would be to specify it as a pure virtual function, since it is pure in the base class, but then we couldn’t create CBox objects.