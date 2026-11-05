# Chapter 37: Casting

# Section 37.1: Checking compatibility without casting

If you need to know whether a value's type extends or implements a given type, but you don't want to actually cast it as that type, you can use the is operator.

```
if(value is int)
{
    Console.WriteLine(value + "is an int");
}
```

# Section 37.2: Cast an object to a base type

Given the following definitions :

```
public interface IMyInterface1
{
    string GetName();
}

public interface IMyInterface2
{
    string GetName();
}

public class MyClass : IMyInterface1, IMyInterface2
{
    string IMyInterface1.GetName()
    {
        return "IMyInterface1";
    }

    string IMyInterface2.GetName()
    {
        return "IMyInterface2";
    }
}
```

Casting an object to a base type example :

```
MyClass obj = new MyClass();

IMyInterface1 myClass1 = (IMyInterface1)obj;
IMyInterface2 myClass2 = (IMyInterface2)obj;

Console.WriteLine("I am : {0}", myClass1.GetName());
Console.WriteLine("I am : {0}", myClass2.GetName());

// Outputs :
// I am : IMyInterface1
// I am : IMyInterface2
```

# Section 37.3: Conversion Operators

In C#, types can define custom Conversion Operators, which allow values to be converted to and from other types using either explicit or implicit casts. For example, consider a class that is meant to represent a JavaScript