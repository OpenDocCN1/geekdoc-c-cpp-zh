```
```csharp
Boolean IReadOnly { get; } // Read-only property
}
```
```

To the CLR, an interface definition is just like a type definition. That is, the CLR will define an internal data structure for the interface type object, and reflection can be used to query features of the interface type. Like types, an interface can be defined at file scope or defined nested within another type. When defining the interface type, you can specify whatever visibility/accessibility (`public`, `protected`, `internal`, etc.) you desire.

By convention, interface type names are prefixed with an uppercase I, making it easy to spot an interface type in source code. The CLR does support generic interfaces (as you can see from some of the previous examples) as well as generic methods in an interface. I will discuss some of the many features offered by generic interfaces later in this chapter and in Chapter 12, “Generics,” in which I cover generics more broadly.

An interface definition can “inherit” other interfaces. However, I use the word *inherit* here rather loosely because interface inheritance doesn’t work exactly as does class inheritance. I prefer to think of interface inheritance as including the contract of other interfaces. For example, the ICollection<T> interface definition includes the contracts of the IEnumerable<T> and IEnumerable interfaces. This means that:

+   - Any class that inherits the ICollection<T> interface must implement all of the methods defined by the ICollection<T>, IEnumerable<T>, and IEnumerable interfaces.
+   - Any code that expects an object whose type implements the ICollection<T> interface can assume that the object’s type also implements the methods of the IEnumerable<T> and IEnumerable interfaces.

# ## Inheriting an Interface

In this section, I’ll show how to define a type that implements an interface, and then I’ll show how to create an instance of this type and use the object to call the interface’s methods. C# actually makes this pretty simple, but what happens behind the scenes is a bit more complicated. I’ll explain what is happening behind the scenes later in this chapter.

The System.IComparable<T> interface is defined (in MSCorLib.dll) as follows:

```
```csharp
public interface IComparableIn<T> {
   Int32 CompareTo(T other);
}
```
```

The following code shows how to define a type that implements this interface and also shows code that compares two Point objects:

```
```csharp
using System;
```
```