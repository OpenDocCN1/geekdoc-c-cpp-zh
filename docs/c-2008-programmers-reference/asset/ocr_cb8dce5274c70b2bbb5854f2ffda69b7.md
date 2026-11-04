Figure 6-7 shows that IntelliSense lists the overloaded constructors in BaseClass.

```
```
public class DerivedClass : BaseClass
{
    //---default constructor---
    public DerivedClass() : base
    {
        Console.WriteLine("Constructor in DerivedClass");
    }
}
```
```

```
```
public class DerivedClass : BaseClass
{
    //---default constructor---
    public DerivedClass() : base
    {
        Console.WriteLine("Constructor in DerivedClass");
    }
}
```
```

Figure 6-7

# Interface Inheritance

When an interface inherits from a base interface, it inherits all the base interface's functions' signatures (but no implementation).

Let's explore the concept of interface inheritance by using the hierarchy of various classes defined earlier in the chapter, starting from the root class Shape, with the Circle and Rectangle classes inheriting from it (the Square class in turn inherits from the Rectangle class), as Figure 6-8 shows.

![](bbox=[0.35, 0.65, 0.75, 0.92])

Figure 6-8