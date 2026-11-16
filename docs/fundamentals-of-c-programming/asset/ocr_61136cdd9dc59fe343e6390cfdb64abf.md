```
Listing 17.27: ellipse.h

#ifndef ELLIPSE_H_
#define ELLIPSE_H_

#include "shape.h"

class Ellipse: public Shape {
protected:
    double major_radius; // The longer radius of the ellipse
    double minor_radius; // The shorter radius of the ellipse
public:
    Ellipse(double major, double minor);
    double span() const override;
    double area() const override;
};

#endif
```

```
Listing 17.28: ellipse.cpp

// File ellipse.cpp

#include "ellipse.h"
#include <algorithm> // For max function

// PI is local to this file
static const double PI = 3.14159;

// Note: This constructor does not enforce
// major_axis >= minor_axis
Ellipse::Ellipse(double major, double minor):
    major_radius(major), minor_radius(minor) {}

// Greatest distance across is the length of the longer radius
double Ellipse::span() const {
    return std::max(major_radius, minor_radius);
}

double Ellipse::area() const {
    return PI * major_radius * minor_radius;
}
```

A circle is just an ellipse with equal major and minor radii. Listing 17.29 (circle.h) and Listing 17.30 (circle.cpp) define the Circle class.

```
Listing 17.29: circle.h

#ifndef CIRCLE_H_
#define CIRCLE_H_

#include "ellipse.h"
```