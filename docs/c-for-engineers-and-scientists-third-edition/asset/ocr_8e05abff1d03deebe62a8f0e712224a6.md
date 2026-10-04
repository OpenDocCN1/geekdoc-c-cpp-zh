# 650 Class Functions and Conversions

# Program 11.14

```
#include <iostream>
#include <cmath>
using namespace std;

const double PI = 2.0 * asin(1.0);

// class declaration section
class Circle {
protected:
    double radius;
public:
    Circle(double r = 1.0); // constructor
    double calcval();
};

// class implementation section for Circle
Circle::Circle(double r) // constructor {
    radius = r;
}

// calculate the area of a circle
double Circle::calcval() {
    return PI * radius;
}

// class declaration section where Cylinder is derived from Circle
class Cylinder : public Circle {
protected:
    double length; // add one additional data member
public:
    // two additional member functions
    Cylinder(double r = 1.0, double l = 1.0) : Circle(r), length(l) {}
    double calcval();
};

// class implementation section for Cylinder
double Cylinder::calcval() {
    return (length * Circle::calcval()); // note the base function call
}
```

![](bbox=[0.117, 0.106, 0.183, 0.153])

![](bbox=[0.843, 0.893, 0.876, 0.911])