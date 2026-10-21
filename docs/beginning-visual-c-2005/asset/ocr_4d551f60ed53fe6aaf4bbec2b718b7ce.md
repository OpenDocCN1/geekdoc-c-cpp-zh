# Virtual Functions

Look more closely at the behavior of inherited member functions and their relationship with derived class member functions. You could add a function to the CBox class to output the volume of a CBox object. The simplified class then becomes:

```
// Box.h in Ex9_06
#pragma once
#include <iostream>
using std::cout;
using std::endl;

class CBox  // Base class
{
public:
    // Function to show the volume of an object
    void ShowVolume() const
    {
        cout << endl << "CBox usable volume is " << Volume();
    }

    // Function to calculate the volume of a CBox object
    double Volume() const
    {
        return m_Length*m_Width*m_Height;
    }

    // Constructor
    CBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
    :m_Length(lv), m_Width(wv), m_Height(hv) {}

protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

Now you can output the usable volume of a CBox object just by calling the ShowVolume() function for any object for which you require it. The constructor sets the data member values in the initialization list, so no statements are necessary in the body of the function. The data members are as before and are specified as protected, so they are accessible to the member functions of any derived class.

Suppose you want to derive a class for a different kind of box called CGlassBox, to hold glassware. The contents are fragile, and because packing material is added to protect them, the capacity of the box is less than the capacity of a basic CBox object. You therefore need a different Volume() function to account for this, so you add it to the derived class:

```
// GlassBox.h in Ex9_06
#pragma once
#include "Box.h"

class CGlassBox: public CBox  // Derived class
{
public:
    // Constructor
    CGlassBox(double lv = 1.0, double wv = 1.0, double hv = 1.0)
    : CBox(lv, wv, hv) {}

    // Function to calculate the volume of a CGlassBox object
    double Volume() const
    {
        return 0.8 * CBox::Volume();
    }
};
```