# Classes 49

Example 61 Constructor Overloading: Calling Another Constructor
Adding a new constructor to the Point class (example 43) overloads its constructors. The old constructor signature is Point(int, int), and the new ones are Point() and Point(Point). The latter makes a copy of the point p by calling the old constructor using the syntax : this(p.x, p.y).

```
public class Point {
    protected internal int x, y;
    public Point(int x, int y) // //loaded constructor
        { this.x = x; this.y = y; } // Overloaded constructor
    public Point()
    { }
    public Point(Point p) // Overloaded constructor
        { this(p.x, p.y); } // Calls the first constructor
    public void Move(int dx, int dy)
        { x += dx; y += dy; }
    public override string ToString()
        { return "(" + x + ", " + y + "); }
}
```

Example 62 Calling a Base Class Constructor
The constructor in the ColoredPoint subclass (example 147) calls its base class constructor using the syntax : base(x, y) in the header of the constructor declaration.

Example 63 The Execution Order of Field Initializers and Constructor Bodies
Evaluating new C() will execute the instance field initializers in class C, execute the instance field initializers in class B, execute the body of the B() constructor, execute the body of the C(int) constructor, and finally execute the body of the C(). That is, it will print 1 2 3 4 5 6 7.

```
class B {
    public readonly int fb1 = Print(3);
    public B(int k) { Print(5); }
    public readonly int fb2 = Print(4);
    public static int Print(int i) { Console.Write(i + " "); return i; }
}

class C : B {
    public readonly int fc1 = Print(1);
    public C() : this(0) { Print(7); }
    public C(int k) : base(k) { Print(6); }
    public readonly int fc2 = Print(2);
}
```