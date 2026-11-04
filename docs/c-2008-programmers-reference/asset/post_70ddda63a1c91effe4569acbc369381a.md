
## Part I: C# Fundamentals

What happens if you have a Method() having the same signature as another one in the base class, such as the following?

```
public class DerivedClass : BaseClass
{
    //---overloads the method with the same parameter list---
    public void Method(int num)
    {
        Console.WriteLine("Number in DerivedClass is " + num);
    }

    //---overloads the method
    public void Method(char ch)
    {
        Console.WriteLine("Character in DerivedClass is " + ch);
    }
}
```

In this case, Method(int num) in DerivedClass will hide the same method in BaseClass, as the following printout proves:

```
DerivedClass d = new DerivedClass();

//---prints out: Number in DerivedClass is 5---
d.Method(5);

//---prints out: String in BaseClass is This is a string---
d.Method("This is a string");

//---prints out: Character in DerivedClass is C---
d.Method('C');
```

If hiding Method(int num) in BaseClass is your true intention, use the new keyword to denote that as follows (or else the compiler will issue a warning):

```
//---overloads the method with the same parameter list
public new void Method(int num)
{
    Console.WriteLine("Number in DerivedClass is " + num);
}
```

> In C#, you use the new keyword to hide methods in the base class by signature. C# does not support hiding methods by name as is possible in VB.NET by using the Shadows keyword.

The following table summarizes the different keywords used for inheritance.

| Modifier | Description |
|---|---|
| new | Hides an inherited method with the same signature. |
| static | A member that belongs to the type itself and not to a specific object. |
| virtual | A method that can be overridden by a derived class. |
| abstract | Provides the signature of a method / class but does not contain any implementation. |
| override | Overrides an inherited virtual or abstract method. |
| sealed | A method that cannot be overridden by derived classes; a class that cannot be inherited by other classes. |
| extern | An "extern" method is one in which the implementation is provided elsewhere and is most commonly used to provide definitions for methods invoked using .NET interop. |

## Overloading Operators

Besides overloading methods, C# also supports the overloading of operators (such as +, -, /, and *). Operator overloading allows you to provide your own operator implementation for your specific type. To see how operator overloading works, consider the following program containing the Point class representing a point in a coordinate system:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace OperatorOverloading
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

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
}
```

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

The operator keyword overloads a built-in operator. In this example, the overloaded + operator allows it to “add” two Point objects by adding the result of their DistanceFromOrigin() methods:

```csharp
static void Main(string[] args)
{
    Point ptA = new Point(4, 5);
    Point ptB = new Point(2, 7);

    Console.WriteLine(ptA + ptB); //---13.6832341267134---
    Console.ReadLine();
}
```

You can also use the operator keyword to define a conversion operator, as the following example shows:

```csharp
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

    public static implicit operator double(Point pt)
    {
        return (pt.X / pt.Y);
    }
}
```

Here, the implicit keyword indicates that you want to implicitly perform a conversion of the Point class to a double value (this value is defined to be the ratio of the X and Y coordinates).

Now when you assign a Point object to a double variable, the ratio of the X and Y coordinates is assigned automatically, as the following statements prove:

```csharp
static void Main(string[] args)
{
    Point ptA = new Point(4, 5);
    Point ptB = new Point(2, 7);

    double ratio = ptA; //---implicitly convert to a double type---
}
```

(continued)

```
ptB = ptA;            //---assign to another Point object---
Console.WriteLine(ratio);    //---0.8---
Console.WriteLine((double)ptB); //---0.8---

    Console.ReadLine();
```

## Extension Methods (C# 3.0)

Whenever you add additional methods to a class in previous versions of C#, you need to subclass it and then add the required method. For example, consider the following predefined (meaning you cannot modify it) classes:

```
public abstract class Shape
{
    //---properties---
    public double length { get; set; }
    public double width { get; set; }

    //---make this method as virtual---
    public virtual double Perimeter()
    {
        return 2 * (this.length + this.width);
    }

    //---abstract method---
    public abstract double Area();
}

public class Rectangle : Shape
{
    public override sealed double Area()
    {
        return this.length * this.width;
    }
}
```

The only way to add a new method Diagonal() to the Rectangle class is to create a new class that derives from it, like this:

```
public class NewRectangle : Rectangle
{
    public double Diagonal()
    {
        return Math.Sqrt(Math.Pow(this.length, 2) + Math.Pow(this.width, 2));
    }
}
```

In C# 3.0, you just use the new extension method feature to add a new method to an existing type. To add the Diagonal() method to the existing Rectangle class, define a new static class and define the extension method (a static method) within it, like this:

```
public static class MethodsExtensions
{
    public static double Diagonal(this Rectangle rect)
    {
        return Math.Sqrt(Math.Pow(rect.length, 2) + Math.Pow(rect.width, 2));
    }
}
```

In this example, Diagonal() is the extension method that is added to the Rectangle class. You can use the Diagonal() method just like a method from the Rectangle class:

```
Rectangle r = new Rectangle();
r.length = 4;
r.width = 5;
//---prints out: 6.40312423743285---
Console.WriteLine(r.Diagonal());
```

The first parameter of an extension method is prefixed by the this keyword, followed by the type it is extending (Rectangle in this example, indicating to the compiler that this extension method must be added to the Rectangle class). The rest of the parameter list (if any) is then the signature of the extension method. For example, to pass additional parameters into the Diagonal() extension method, you can declare it as:

```
public static double Diagonal(this Rectangle rect, int x, int y)
{
    //---additional implementation here---
    return Math.Sqrt(Math.Pow(rect.length, 2) + Math.Pow(rect.width, 2));
}
```

To call this modified extension method, simply pass in two arguments, like this:

```
Console.WriteLine(r.Diagonal(3,4));
```

Figure 6-4 shows IntelliSense providing a hint on the parameter list.

![](img/a977a875c7c627b45d939729705a252e_222_0.png)

Although an extension method is a useful new feature in the C# language, use it sparingly. If an extension method has the same signature as another method in the class it is trying to extend, the method in the class will take precedence and the extension method will be ignored.
