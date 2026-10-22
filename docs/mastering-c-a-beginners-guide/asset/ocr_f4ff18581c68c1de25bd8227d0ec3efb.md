binding. Example of the runtime polymorphism would be:

```
using System;
public abstract class Shape
{
    protected int x;
    protected int y;
    public abstract int Area();
}
public class Rectangle : Shape
{
    public Rectangle(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
    public override int Area()
    {
    }
}
public class Square: Shape
{
    public Square(int x)
    {
        this.x = x;
    }
    public override int Area()
    {
        return this.x * this.x;
    }
}
public class Polymorphism
```