You define a reference class using the ref class keyword — both words together separated by one or more spaces represent a single keyword. Here’s the CBox class from the Ex7_07 example redefined as a reference class.

```
ref class Box
{
    public:
        // No-arg constructor supplying default field values
        Box(): Length(1.0), Width(1.0), Height(1.0)
        {
            Console::WriteLine(L"No-arg constructor called.");
        }
        // Constructor definition using an initialisation list
        Box(double lv, double bv, double hv):
                    Length(lv), Width(bv), Height(hv)
        {
            Console::WriteLine(L"Constructor called.");
        }
        // Function to calculate the volume of a box
        double Volume()
        {
            return Length*Width*Height;
        }
    private:
        double Length;            // Length of a box in inches
        double Width;             // Width of a box in inches
        double Height;            // Height of a box in inches
};
```

Note first that I have removed the C prefix for the class name and the m_ prefix for member names because this notation is not recommended for C++/CLI classes. You cannot specify default values for function and constructor parameters in C++/CLI classes so you have to add a no-arg constructor to the Box class to fulfill this function. The no-arg constructor just initializes the three private fields with 1.0.

# Try It Out Using a Reference Class Type

Here’s an example that uses the Box class that you saw in the previous section.

```
// Ex7_15.cpp : main project file.
// Using the Box reference class type

#include "stdafx.h"

using namespace System;
```

```
ref class Box
{
    public:
        // No-arg constructor supplying default field values
        Box(): Length(1.0), Width(1.0), Height(1.0)
        {
```