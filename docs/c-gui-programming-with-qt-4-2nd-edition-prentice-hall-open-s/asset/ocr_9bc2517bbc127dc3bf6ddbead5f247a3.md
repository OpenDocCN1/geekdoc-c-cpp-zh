For some one-parameter constructors, the automatic conversion makes little sense. We can disable it by declaring the constructor with the explicit keyword:

```
class MyVector
public:
    explicit MyVector(int size);
    ...
};
```

# Operator Overloading

C++ allows us to overload functions, meaning that we can declare several functions with the same name in the same scope, as long as they have different parameter lists. In addition, C++ supports operator overloading—the possibility of assigning special semantics to built-in operators (such as +, <<, and []) when they are used with custom types.

We have already seen a few examples of overloaded operators. When we used << to output text to cout and cerr, we didn't trigger C++'s left-shift operator, but rather a special version of the operator that takes an ostream object (such as cout and cerr) on the left side and a string (alternatively, a number or a stream manipulator such as endl) on the right side and returns the ostream object, allowing calls in a row.

The beauty of operator overloading is that we can make custom types behave just like built-in types. To show how operator overloading works, we will overload +=, =, and to work on Point2D objects:

Code View:

```
#ifndef POINT2D_H
#define POINT2D_H

class Point2D
public:
    Point2D();
    Point2D(double x, double y);

    void setX(double x);
    void setY(double y);
    double x() const;
    double y() const;
```