You can also seal methods so that other derived classes cannot override the implementation that you have provided in the current class. For example, recall that the Rectangle class provides the implementation for the abstract Area() method defined in the Shape class:

```
```csharp
public class Rectangle : Shape
{
    public override double Area()
    {
        return this.length * this.width;
    }
}
```
```

To prevent the derived classes of Rectangle (such as Square) from modifying the Area() implementation, prefix the method with the sealed keyword:

```
```csharp
public class Rectangle : Shape
{
    public override sealed double Area()
    {
        return this.length * this.width;
    }
}
```
```

Now if you try to override the Area() method in the Square class, you get an error:

```
```csharp
public sealed class Square : Rectangle
{
    //---Error: Area() is sealed in Rectangle class---
    public override double Area()
    {
        //---implementation here---
    }
}
```
```

# Overloading Methods

When you have multiple methods in a class having the same name but different signatures (parameters), they are known as overloaded methods. Consider the following class definition:

```
```csharp
public class BaseClass
{
    public void Method(int num)
    {
        Console.WriteLine("Number in BaseClass is " + num);
    }

    public void Method(string st)
    {
        Console.WriteLine("String in BaseClass is " + st);
    }
}
```
```