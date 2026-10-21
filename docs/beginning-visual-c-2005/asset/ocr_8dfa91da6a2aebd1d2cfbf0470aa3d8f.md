# Chapter 9

```
{ return m_Length*m_Width*m_Height; }

// Constructor
Box() : m_Length(1.0), m_Width(1.0), m_Height(1.0) {}

// Constructor
Box(double lv, double wv, double hv)
    : m_Length(lv), m_Width(wv), m_Height(hv) {}

protected:
    double m_Length;
    double m_Width;
    double m_Height;
};
```

A base class for a ref class is always public and the public keyword is assumed by default. You can specify the base class explicitly as public but it is not necessary to do so. A base class to a ref class cannot be specified as anything other than public. Because you cannot supply default values for parameters as in the native C++ version of the class, you define the no-arg constructor so that it initializes all three fields to 1.0. The Box class defines the Volume() function as an override to the inherited base class version. You must always specify the override keyword when you want to override a function in the base class. If the Box class did not implement the Volume() function, it would be abstract and you would need to specify it as such to compile the class successfully.

Here’s how the GlassBox class definition looks:

```
// GlassBox.h for Ex9_14
#pragma once
#include "Box.h"                // For Box

ref class GlassBox : Box          // Derived class
{
public:
    // Function to calculate volume of a GlassBox
    // allowing 15% for packing
    virtual double Volume() override
    { return 0.85*m_Length*m_Width*m_Height; }

    // Constructor
    GlassBox(double lv, double wv, double hv): Box(lv, wv, hv) {}
};
```

The base class is Box, which is public by default. The rest of the class is essentially the same as the original.

Here’s the Stack class definition:

```
// Stack.h for Ex9_14
// A push-down stack to store objects of any ref class type
#pragma once

ref class Stack
```