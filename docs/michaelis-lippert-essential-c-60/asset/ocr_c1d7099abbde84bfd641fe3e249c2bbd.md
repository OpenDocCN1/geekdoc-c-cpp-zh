In this example, the extension method is not on for an `IListable` parameter (although it could have been), but rather for an `IListable[]` parameter. This demonstrates that C# allows extension methods not only on an instance of a particular type, but also on a collection of those objects. Support for extension methods is the foundation on which LINQ is implemented. `IEnumerable` is the fundamental interface that all collections implement. By defining extension methods for `IEnumerable`, LINQ support was added to all collections. This radically changed programming with collections; we will explore this topic in detail in Chapter 14.

# Implementing Multiple Inheritance via Interfaces

As Listing 7.3 demonstrated, a single class can implement any number of interfaces in addition to deriving from a single class. This feature provides a possible workaround for the lack of multiple inheritance support in C# classes. The process uses aggregation as described in the preceding chapter, but you can vary the structure slightly by adding an interface to the mix, as shown in Listing 7.11.

```
**LISTING 7.11: Working around Single Inheritance Using Aggregation with Interfaces**

```csharp
public class PdaItem
{
    // ...
}

interface IPerson
{
    string FirstName
    {
        get;
        set;
    }

    string LastName
    {
        get;
        set;
    }
}

public class Person : IPerson
{
    // ...
}
```
```

![](bbox=[0.885, 0.256, 1.0, 0.294])