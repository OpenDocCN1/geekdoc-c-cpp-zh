```
```csharp
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

  /* A default constructor. This automatically invokes
     the default constructor of TwoDShape. */
  public Triangle() {
    Style = "null";
  }

  // Constructor that takes three arguments.
  public Triangle(string s, double w, double h) : base(w, h) {
    Style = s;
  }

  // Construct an isosceles triangle.
  public Triangle(double x) : base(x) {
    Style = "isosceles";
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

class Shapes5 {
  static void Main() {
    Triangle t1 = new Triangle();
    Triangle t2 = new Triangle("right", 8.0, 12.0);
    Triangle t3 = new Triangle(4.0);

    t1 = t2;

    Console.WriteLine("Info for t1: ");
    t1.ShowStyle();
    t1.ShowDim();
    Console.WriteLine("Area is " + t1.Area());
  }
}
```
```