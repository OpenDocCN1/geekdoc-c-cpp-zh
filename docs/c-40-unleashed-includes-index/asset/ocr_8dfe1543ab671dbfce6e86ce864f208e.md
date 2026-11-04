```
```csharp
public double Radius { get; private set; }

public override double Area
{
    get { return Math.PI * Radius * Radius; }
}

public override double Circumference
{
    get { return Math.PI * 2 * Radius; }
}
}

class Square : Shape
{
    public Square(double side)
    {
        Side = side;
    }

    public double Side { get; private set; }

    public override double Area
    {
        get { return Side * Side; }
    }

    public override double Circumference
    {
        get { return 4 * Side; }
    }
}
```
```

As we enter this code, IntelliSense will help us by suggesting the members that can still be overridden. With this code in place, we can write polymorphic code:

```
```csharp
Shape s1 = new Circle(2.0);
Console.WriteLine(s1.Area);
Shape s2 = new Square(3.0);
Console.WriteLine(s2.Circumference);
```
```

# Sealing and Hiding: Take Two

As previously mentioned, the sealed keyword prevents a class from being derived any further. We can also apply such specialization prevention at a more granular level of