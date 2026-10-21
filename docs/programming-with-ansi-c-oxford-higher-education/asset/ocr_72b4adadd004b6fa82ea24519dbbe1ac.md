are the implementation of the formulae that have been mentioned earlier. However, it is not possible to write PPoint1 = CPoint1 because we do not have any constructor in the Polar class for the Cartesian class. If both the conversions are needed, one way is to use operators as described in Section 6.12.6.

# 6.11.6 Conversion of Object Type using Conversion Functions

When a native object needs to be converted into a foreign object, operator functions (conversion functions) are used. They can be used in the same manner as used while converting to a basic type from an object. Program 6.15 shows the use of operator functions.

# PROGRAM 6.15 Cartesian to polar object conversion using operator function

```
//CartesianToPolar1.cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;
class Cartesian;
class Polar
{
    double Radius;
    double Angle;
public:
    Polar(double TempRadius = 0, double TempAngle = 0)
    {
        Radius = TempRadius;
        Angle = TempAngle;
    }
    double GetRadius()
    {
        Return Radius;
    }
    double GetAngle()
    {
        return Angle;
    }
    void Show()
    {
        cout << "(" << Radius <<", "<< Angle <<")\n";
    }
};
class Cartesian
{
    double X;
    double Y;
public:
    Cartesian(double TempX = 0, double TempY = 0)
    {
        X = TempX;
        Y = TempY;
    }
    Cartesian(Polar PolarPoint)
    {
```