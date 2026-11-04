(continued)

```
public double DistanceFromOrigin()
{
    return (Math.Sqrt(Math.Pow(this.X, 2) + Math.Pow(this.Y, 2)));
}
}
```

The Point class contains two public properties (X and Y), a constructor, and a method — DistanceFromOrigin().

If you constantly perform calculations where you need to add the distances of two points (from the origin), your code may look like this:

```
static void Main(string[] args)
{
    Point ptA = new Point(4, 5);
    Point ptB = new Point(2, 7);
    double distanceA, distanceB;
    distanceA = ptA.DistanceFromOrigin(); //---6.40312423743285---
    distanceB = ptB.DistanceFromOrigin(); //---7.28010988928052---
    Console.WriteLine(distanceA + distanceB); //---13.6832341267134---
    Console.ReadLine();
}
```

A much better implementation is to overload the + operator for use with the Point class. To overload the + operator, define a public static operator within the Point class as follows:

```
class Point
{
    public Single X { get; set; }
    public Single Y { get; set; }
    public Point(Single X, Single Y)
    {
        this.X = X;
        this.Y = Y;
    }
    public double DistanceFromOrigin()
    {
        return (Math.Sqrt(Math.Pow(this.X, 2) + Math.Pow(this.Y, 2)));
    }
    public static double operator +(Point A, Point B)
    {
        return (A.DistanceFromOrigin() + B.DistanceFromOrigin());
    }
}
```