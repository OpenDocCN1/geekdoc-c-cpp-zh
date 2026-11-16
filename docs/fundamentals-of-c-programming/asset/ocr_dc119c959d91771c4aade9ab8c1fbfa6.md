# Listing 17.20: shape.h

```
#ifndef SHAPE_H_
#define SHAPE_H_

/*
 * Shape is the base class for all shapes
 */
class Shape {
public:
    // Longest distance across the shape
    virtual double span() const = 0;
    // The shape's area
    virtual double area() const = 0;
};
#endif
```

The "assignment to zero" of the two virtual methods in the `Shape` class make them special; they are called *pure virtual methods* or *pure virtual functions*. This special syntax signifies that these methods have no implementations. It is not possible to provide a body for these methods. A class that contains at least one pure virtual method is an *abstract class*. It is not possible to create an instance of an abstract class. The compiler enforces this restriction; the following statement:

```
Shape myShape; // Illegal
```

is illegal. A non-abstract class is called a *concrete class*. All the classes we have seen to this point except for `Shape` have been concrete classes.

An abstract class represents an abstract concept. `Shape` is an abstract concept. We can have circles, rectangles, and lots of other kinds of shapes, but can we have something that is "just a shape" without being a particular kind of shape? Even though we cannot create instances of abstract classes, abstract classes are useful for organizing a class hierarchy.

We can derive a concrete class from our `Shape` class as shown in Listing 17.21 (rectangle.h).

# Listing 17.21: rectangle.h

```
#ifndef RECTANGLE_H_
#define RECTANGLE_H_

#include "shape.h"

class Rectangle: public Shape {
protected:
    double length;
    double width;
public:
    Rectangle(double len, double wid);
    // Length of the longer side
    double span() const override;
    double area() const override;
};
```