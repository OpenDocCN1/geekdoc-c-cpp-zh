```
public int X
{
    get { return x; }
    set { x = value; }
}
public int Y
{
    get { return y; }
    set { y = value; }
}
}
struct Rectangle
{
    Point a, b;
    public Rectangle(Point a, Point b)
    {
        this.a = a;
        this.b = b;
    }
    public Point A
    {
        get { return a; }
        set { a = value; }
    }
    public Point B
    {
        get { return b; }
        set { b = value; }
    }
}
```

in the example

```
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```

the assignments to p.X, p.Y, r.A, and r.B are permitted because p and r are variables. However, in the example

```
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```

the assignments are all invalid because r.A and r.B are not variables.