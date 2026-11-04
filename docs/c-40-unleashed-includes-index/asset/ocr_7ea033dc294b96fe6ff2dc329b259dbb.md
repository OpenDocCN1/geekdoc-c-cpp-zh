pt.cs(9,1): error CS1612: Cannot modify the return value of 'Kid.Location'
    because it is not a variable
pt.cs(10,1): error CS1612: Cannot modify the return value of 'Kid.Location'
    because it is not a variable

Instead of trying this, it's better to prevent changes to the Point object and just have the user substitute the Location property value for an entirely new Point instead:

```
using System;

class Program
{
    static void Main()
    {
        var kid = new Kid();
        Console.WriteLine(kid.Location.X + ", " + kid.Location.Y);
        kid.Location = new Point(3, 4);
        Console.WriteLine(kid.Location.X + ", " + kid.Location.Y);
    }
}

class Kid
{
    public Point Location { get; set; }
}

struct Point
{
    private int _x;
    private int _y;

    public Point(int x, int y)
    {
        _x = x;
        _y = y;
    }

    public int X { get { return _x; } }
    public int Y { get { return _y; } }
}
```

Alternatively, turn the location's type into a reference type. However, doing so blindly just to restore the mutability property usually is not a good idea. Always think about the characteristic of the type first: Does it represent a value, or is it something one wants to refer to? When the former is true, a struct is the right choice, and declaring the value type as immutable is highly recommended.