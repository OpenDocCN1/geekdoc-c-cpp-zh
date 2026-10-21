# Chapter 9

```
// Function to calculate volume of a CGlassBox
// allowing 15% for packing
double Volume() const
{ return 0.85*m_Length*m_Width*m_Height; }

// Constructor
CGlassBox(double lv, double wv, double hv): CBox(lv, wv, hv){}
};
```

There could conceivably be other additional members of the derived class, but we’ll keep it simple and concentrate on how the inherited functions work for the moment. The constructor for the derived class objects just calls the base class constructor in its initialization list to set the data member values. No statements are necessary in its body. You have included a new version of the Volume() function to replace the version from the base class, the idea being that you can get the inherited function ShowVolume() to call the derived class version of the member function Volume() when you call it for an object of the class CGlassBox.

# Try It Out Using an Inherited Function

Now see how your derived class works in practice. You can try this out very simply by creating an object of the base class and an object of the derived class with the same dimensions and then verifying that the correct volumes are being calculated. The main() function to do this is as follows:

```
// Ex9_06.cpp
// Behavior of inherited functions in a derived class
#include <iostream>
#include "GlassBox.h"                // For CBox and CGlassBox
using std::cout;
using std::endl;

int main()
{
    CBox myBox(2.0, 3.0, 4.0);           // Declare a base box
    CGlassBox myGlassBox(2.0, 3.0, 4.0); // Declare derived box - same size

    myBox.ShowVolume();                 // Display volume of base box
    myGlassBox.ShowVolume();            // Display volume of derived box

    cout << endl;
    return 0;
}
```

# How It Works

If you run this example, it produces the following output:

```
CBox usable volume is 24
CBox usable volume is 24
```

This isn’t only dull and repetitive, it’s also disastrous. It isn’t working the way you want at all, and the only interesting thing about it is why. Evidently, the fact that the second call is for an object of the