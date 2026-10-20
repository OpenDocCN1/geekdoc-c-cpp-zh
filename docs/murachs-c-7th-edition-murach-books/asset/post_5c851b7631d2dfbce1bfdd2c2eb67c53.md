
## 15 How to work with interfaces and generics

This chapter starts by showing you how to use interfaces. Interfaces are similar to abstract classes, but they have some advantages that make them easier to create and more flexible to use. Then, this chapter shows you how to use generics so you can code your own collections that work like the generic .NET collections presented in chapter 8. Along the way, you’ll learn how to work with the generic interfaces that are used with generic collections.

- How to work with interfaces................................................496
- An introduction to interfaces................................................496
- Some of the interfaces defined by .NET.......................................498
- How to create an interface...................................................500
- How to implement an interface................................................502
- A Product class that implements the ICloneable interface.....................504
- How to use an interface as a parameter.......................................506
- How to work with default methods.............................................508
- How to work with static methods and fields..................................508
- How to work with generics....................................................510
- How to code a class that defines a generic collection.......................510
- Some of the generic interfaces defined by .NET..............................514
- How to implement the IComparable<> interface...............................516
- How to use constraints.......................................................518
- How to implement the IEnumerable<> interface...............................520
- How to code an interface that uses generics.................................522
- Perspective...................................................................524

### The IDisplayable interface

```csharp
interface IDisplayable
{
    string GetDisplayText(string sep);
}
```

### A Product class that implements the IDisplayable interface

```csharp
public class Product : IDisplayable
{
    public string Code { get; set; }
    public string Description { get; set; }
    public decimal Price { get; set; }

    public Product(string Code, string Description, decimal Price)
    {
        this.Code = Code;
        this.Description = Description;
        this.Price = Price;
    }

    public string GetDisplayText(string sep) =>
        this.Code + sep + this.Description + sep + this.Price.ToString("c");
}
```

### Code that uses the IDisplayable interface

```csharp
IDisplayable product = new Product("C#", "Murach's C#", 59.50m);
Debug.WriteLine(product.GetDisplayText("\n"));
```

### A comparison of interfaces and abstract classes

- Both interfaces and abstract classes can provide signatures for properties and methods that a class must implement.
- Both interfaces and abstract classes can implement some or all of their properties and methods.
- An abstract class can use instance variables and constants as well as static variables and constants. An interface can only use static variables and constants.
- A class can inherit only one class (including abstract classes), but a class can implement more than one interface.

### Description

- An *interface* consists of a set of signatures for one or more methods, properties, indexers, or events.
- With C# 8.0 and later, an interface can provide implementation for its *default interface members*. Default interface members may be overridden by any class that *implements* the interface, and all non-default interface members must be defined by those classes. By convention, interface names begin with the letter I to distinguish them from classes.
- To implement an interface, a class must name the interface on the class declaration, and it must provide an implementation for every non-default member of the interface.

In figure 15-1, the interface name begins with the capital letter I. Although that's not a requirement, it's a coding convention that's followed by all the .NET interfaces, and it helps you distinguish between interfaces and classes. So when you create your own interfaces, we recommend that you follow this coding convention.

### Some of the interfaces defined by .NET

.NET defines hundreds of interfaces. Fortunately, most of them are intended for use by other .NET classes. As a result, you don't need to learn them all. To give you an idea of what some of these interfaces do, though, figure 15-2 lists a few of them.

The first table in this figure lists four general purpose .NET interfaces: ICloneable, IComparable, IConvertible, and IDisposable. Of these four, the one you’re most likely to implement is ICloneable. This interface lets you create objects that can produce copies of themselves. It consists of a single method (Clone()) that returns a copy of the object. You’ll see an example of a Product class that implements this interface in figure 15-5.

While the other three interfaces in the first table are commonly used by .NET interfaces, you typically won’t need to implement any of them for the classes that you code. For example, the IComparable interface provides a standard way for an object to compare itself with another object. However, most business classes don’t have any real basis for determining whether one instance of the class is greater than, equal to, or less than another.

The second table in this figure lists several interfaces that are used by collection classes in the System.Collections namespace. The most important of these are IEnumerable and IEnumerator, which provide a standard mechanism for iterating through the items of a collection. If you implement these interfaces for a collection, you can then use the class in a foreach statement. In fact, this is the main benefit of implementing the IEnumerable and IEnumerator interfaces.

The other three interfaces listed in the second table provide standard ways to implement collection features. The ICollection interface defines a basic collection that maintains a count of items, can be synchronized, and can copy the collection items to an array. The IList interface adds an indexer and methods to add, clear, and remove items. And the IDictionary interface implements a dictionary, which can be used to maintain key/value pairs.

When reviewing the interfaces in this figure, keep in mind that these are the interfaces that were used by .NET prior to the introduction of generics. As a result, they aren’t used by the generic collection classes in the System.Collections.Generic namespace. Instead, the generic collection classes use the generic interfaces you’ll learn about later in this chapter.

### Commonly used .NET interfaces

| Interface | Members | Description |
| --- | --- | --- |
| ICloneable | object Clone() | Creates a duplicate copy of an object. |
| IComparable | int CompareTo(object) | Compares objects. |
| IConvertible | TypeCode GetTypeCode()<br>decimal ToDecimal()<br>int ToInt32()<br>... | Converts an object to one of the common language runtime types, such as Int32, Decimal, or Boolean. |
| IDisposable | void Dispose() | Frees unmanaged resources. |

### Commonly used .NET interfaces for collections

| Interface | Members | Description |
| --- | --- | --- |
| IEnumerable | IEnumerator GetEnumerator() | Gets an enumerator for the collection. |
| IEnumerator | object Current<br>bool MoveNext()<br>void Reset() | Defines an enumerator that provides read-only, forward-only access to a collection. |
| ICollection | int Count<br>bool IsSynchronized<br>object SyncRoot<br>void CopyTo(array, int) | Provides basic properties for an enumerable collection. This interface inherits IEnumerable. |
| IList | Item[int]<br>int Add(object)<br>void Clear()<br>void Remove(object)<br>void RemoveAt(int) | Manages a basic list of objects. This interface inherits ICollection and IEnumerable. |
| IDictionary | Item[object]<br>ICollection Keys<br>ICollection Values<br>void Add(object, object)<br>void Remove(object)<br>void Clear() | Manages a collection of key/value pairs. This interface inherits ICollection and IEnumerable. |

### Description

- .NET defines many interfaces that you can implement in your classes. However, many of these interfaces have been updated by the generic interfaces that are presented later in this chapter.
- The ICollection interface inherits the IEnumerable interface, which means that any class that implements ICollection must also implement IEnumerable. Similarly, the IList and IDictionary interfaces inherit ICollection and IEnumerable.
- This table only lists the most important members of each interface. For a complete description of these interfaces and a list of their members, see the online documentation.
- The interfaces for working with Collections are stored in the System.Collections namespace.

Figure 15-2 Some of the interfaces defined by .NET
