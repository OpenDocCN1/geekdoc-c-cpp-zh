(continued)

```
//return base.length * base.width;
}
    public override double Perimeter()
    {
        //---invokes the Perimeter() method in the Shape class---
        return base.Perimeter();
    }
}
```

You can now use the Rectangle class like this:

```
Rectangle r = new Rectangle();
r.length = 4;
r.width = 5;
Console.WriteLine(r.Perimeter());  //---18---
Console.WriteLine(r.Area());       //---20---
```

*An abstract method can only be defined in an abstract class.*

The base keyword refers to the parent class of a derived class, not the root class. Consider the following example where you have three classes — Class1 inherits from Class2, which in turn inherits from Class1:

```
public class Class1
{
    public virtual void PrintString()
    {
        Console.WriteLine("Class1");
    }
}

public class Class2: Class1
{
    public override void PrintString()
    {
        Console.WriteLine("Class2");
    }
}

public class Class3 : Class2
{
    public override void PrintString()
    {
        base.PrintString();
    }
}
```