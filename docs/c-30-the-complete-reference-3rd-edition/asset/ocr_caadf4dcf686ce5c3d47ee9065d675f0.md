When only the derived class defines a constructor, the process is straightforward: Simply construct the derived class object. The base class portion of the object is constructed automatically using its default constructor. For example, here is a reworked version of Triangle that defines a constructor. It also makes Style private since it is now set by the constructor.

```
~~~csharp
// Add a constructor to Triangle.

using System;

// A class for two-dimensional objects.
class TwoDShape {
    double pri_width;
    double pri_height;

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
    string Style;

    // Constructor.
    public Triangle(string s, double w, double h) {
        Width = w; // init the base class
        Height = h; // init the base class

        Style = s; // init the derived class
    }

    // Return area of triangle.
    public double Area() {
        return Width * Height / 2;
    }

    // Display a triangle's style.
    public void ShowStyle() {
        Console.WriteLine("Triangle is " + Style);
    }
}
~~~
```