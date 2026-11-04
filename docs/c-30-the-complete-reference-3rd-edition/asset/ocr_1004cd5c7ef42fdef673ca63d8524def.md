```
// Constructor.
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

// Extend Triangle.
class ColorTriangle : Triangle {
    string color;

    public ColorTriangle(string c, string s,
                         double w, double h) : base(s, w, h) {
        color = c;
    }

    // Display the color.
    public void ShowColor() {
        Console.WriteLine("Color is " + color);
    }
}

class Shapes6 {
    static void Main() {
        ColorTriangle t1 =
            new ColorTriangle("Blue", "right", 8.0, 12.0);
        ColorTriangle t2 =
            new ColorTriangle("Red", "isosceles", 2.0, 2.0);

        Console.WriteLine("Info for t1: ");
        t1.ShowStyle();
        t1.ShowDim();
        t1.ShowColor();
        Console.WriteLine("Area is " + t1.Area());

        Console.WriteLine();

        Console.WriteLine("Info for t2: ");
        t2.ShowStyle();
        t2.ShowDim();
        t2.ShowColor();
    }
}
```