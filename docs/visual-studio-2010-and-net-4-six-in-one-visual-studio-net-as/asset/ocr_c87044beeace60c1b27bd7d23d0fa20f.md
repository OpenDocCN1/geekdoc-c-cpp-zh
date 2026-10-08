Even static and virtual methods can leverage on generics, as shown here:

```
public class BaseClass
{
    public static void WriteToDebug<T>(T item) { ... }
    public virtual void SomeMethod<T>(T t) { }
}

public class SubClass: BaseClass
{
    public override void SomeMethod<T>(T t) { ... }
}
```

Operators and delegates are implemented as methods behind the scenes, and both of support generics with all the power of generic methods. Here is a small example of defining and consuming generic delegates:

```
public class MyClass<T>
{
    public delegate void GenericDelegate<T>(T t);
    public void SomeMethod(T t) { }
}

// --- Use the delegate
MyClass<int> obj = new MyClass<int>();
MyClass<int>.GenericDelegate del =
el = new MyClass<int>.GenericDelegate(obj.SomeMethod);
del(3);
```

In .NET 2.0, reflection is extended to support generic type parameters. The type System can represent generic types with specific type arguments (closed), or unspecified (open) types.

Also, many types in .NET 2.0 — especially Array had been changed or added to support generics. For example, Array now has new generic methods, and there are many generic collection classes to provide a new and performance-boosted experience related to the old .NET 1.1 collection types.

# Partial Types

The limitation that type definitions to be entirely in one physical file was a bottleneck in C# 1.0, making the life of developers unnecessarily difficult. Large type definitions could not be split, and that was especially disadvantageous for those who used code intensively, because generated code could not be separated from user-defined code.

Partial types solve this issue. By using the partial keyword, class, struct, and interface definitions can be spread out in multiple files. This solves the problem of separation of userdefined and generated code. During compile time the partitions of the type definition are merged, including attributes, base classes and interfaces, and access modifiers.