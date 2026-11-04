```
// X references know only about X members
    x2.a = 19; // OK
//      x2.b = 27; // Error, X doesn't have a b member
}
```

In this program, Y is derived from X. Now, the assignment

```
x2 = y; // OK because Y is derived from X
```

is permissible because a base class reference, x2 in this case, can refer to a derived class object (which is the object referred to by y).

It is important to understand that it is the type of the reference variable—not the type of the object that it refers to—that determines what members can be accessed. That is, when a reference to a derived class object is assigned to a base class reference variable, you will have access only to those parts of the object defined by the base class. This is why you can't access b even when it refers to a Y object. This makes sense because the base class has no knowledge of what a derived class adds to it. This is why the last line of code in the program is commented out.

Although the preceding discussion may seem a bit esoteric, it has some important practical applications. One is described here. The other is discussed later in this chapter, when virtual methods are covered.

An important place where derived class references are assigned to base class variables is when constructors are called in a class hierarchy. As you know, it is common for a class to define a constructor that takes an object of its class as a parameter. This allows the class to construct a copy of an object. Classes derived from such a class can take advantage of this feature. For example, consider the following versions of TwoDShape and Triangle. Both add constructors that take an object as a parameter.

```
// Pass a derived class reference to a base class reference.

using System;

class TwoDShape {
    double pri_width;
    double pri_height;

    // Default constructor.
    public TwoDShape() {
        Width = Height = 0.0;
    }

    // Constructor for TwoDShape.
    public TwoDShape(double w, double h) {
        Width = w;
        Height = h;
    }

    // Construct object with equal width and height.
    public TwoDShape(double x) {
        Width = Height = x;
    }
}
```