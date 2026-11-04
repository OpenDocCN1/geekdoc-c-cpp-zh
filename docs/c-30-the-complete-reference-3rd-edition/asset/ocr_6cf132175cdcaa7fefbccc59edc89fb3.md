To see how a multilevel hierarchy can be useful, consider the following program.
In it, the derived class Triangle is used as a base class to create the derived class called ColorTriangle. ColorTriangle inherits all of the traits of Triangle and TwoDShape and adds a field called color, which holds the color of the triangle.

```
// A multilevel hierarchy.
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

    // Properties for Width and Height.
    public double Width {
        get { return pri_width; }
        set { pri_width = value < 0 ? -value : value; }
    }

    public double Height {
        get { return pri_height; }
        set { pri_height = value < 0 ? -value : value; }
    }

    public void ShowDim() {
        Console.WriteLine("Width and height are " +
            Width + " and " + Height);
    }
}

// A derived class of TwoDShape for triangles.
class Triangle : TwoDShape {
    string Style; // private

    /* A default constructor. This invokes the default
       constructor of TwoDShape. */
    public Triangle() {
        Style = "null";
    }
}
```