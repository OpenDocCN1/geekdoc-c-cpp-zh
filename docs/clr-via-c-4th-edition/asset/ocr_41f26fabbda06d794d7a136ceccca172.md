Although the CLR does allow an interface to define static methods, static fields, constants, and static constructors, a Common Language Specification (CLS)-compliant interface must not have any of these static members because some programming languages aren’t able to define or access them. In fact, C# prevents an interface from defining any of these static members.

In C#, you use the interface keyword to define an interface, giving it a name and its set of instance method signatures. Here are the definitions of a few interfaces defined in the Framework Class Library (FCL).

```
```csharp
public interface IDisposable {
    void Dispose();
}

public interface IEnumerable {
    IEnumerator GetEnumerator();
}

public interface IEnumerable<out T> : IEnumerable {
    new IEnumerator<T> GetEnumerator();
}

public interface ICollection<T> : IEnumerable<T>, IEnumerable {
    void Add(T item);
    void Clear();
    Boolean Contains(T item);
    void CopyTo(T[] array, Int32 arrayIndex);
    Boolean Remove(T item);
    Int32 Count { get; } // Read-only property
    Boolean IsReadOnly { get; } // Read-only property
}
```
```

To the CLR, an interface definition is just like a type definition. That is, the CLR will define an internal data structure for the interface type object, and reflection can be used to query features of the interface type. Like types, an interface can be defined at file scope or defined nested within another type. When defining the interface type, you can specify whatever visibility/accessibility (public, protected, internal, etc.) you want.

By convention, interface type names are prefixed with an uppercase I, making it easy to spot an interface type in source code. The CLR does support generic interfaces (as you can see from some of the previous examples) as well as generic methods in an interface. I will discuss some of the many features offered by generic interfaces later in this chapter and in Chapter 12, “Generics,” in which I cover generics more broadly.

An interface definition can “inherit” other interfaces. However, I use the word inherit here rather loosely because interface inheritance doesn’t work exactly like class inheritance. I prefer to think of interface inheritance as including the contract of other interfaces. For example, the ICollection<T> interface definition includes the contracts of the IEnumerable<T> and IEnumerable interfaces.