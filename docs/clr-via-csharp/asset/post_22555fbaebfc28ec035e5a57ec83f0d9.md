
```csharp
public static void Main() {
    Int32 x = 5;
    Single s = x.ToSingle(null); // Trying to call an IConvertible method
}
```

When compiling this method, the C# compiler produces the following message:
`error CS0117: 'Int32' does not contain a definition for 'ToSingle'.` This error message confuses the developer because it's clearly stating that the `Int32` type doesn't define a `ToSingle` method when, in fact, it does.

To call `ToSingle` on an `Int32`, you must first cast the `Int32` to an `IConvertible`, as shown in the following method:

```csharp
public static void Main() {
    Int32 x = 5;
    Single s = ((IConvertible) x).ToSingle(null);
}
```

Requiring this cast isn't obvious at all, and many developers won't figure this out on their own. But an even more troublesome problem exists: casting the `Int32` value type to an `IConvertible` also boxes the value type, wasting memory and hurting performance. This is the second of the big problems I mentioned at the beginning of this section.

The third and perhaps the biggest problem with EIMIs is that they cannot be called by a derived class. Here is an example:

```csharp
internal class Base : IComparable {

    // Explicit Interface Method Implementation
    Int32 IComparable.CompareTo(Object o) {
        Console.WriteLine("Base's CompareTo");
        return 0;
    }
}

internal sealed class Derived : Base, IComparable {

    // A public method that is also the interface implementation
    public Int32 CompareTo(Object o) {
        Console.WriteLine("Derived's CompareTo");

        // This attempt to call the base class's EIMI causes a compiler error:
        // error CS0117: 'Base' does not contain a definition for 'CompareTo'
        base.CompareTo(o);
        return 0;
    }
}
```

In *Derived's* `CompareTo` method, I try to call `base.CompareTo`, but this causes the C# compiler to issue an error. The problem is that the `Base` class doesn't offer a public or protected `CompareTo` method that can be called; it offers a `CompareTo` method that can be called only by using a variable that is of the **IComparable** type. I could modify **Derived**'s **CompareTo** method so that it looks like this:

```csharp
// A public method that is also the interface implementation
public Int32 CompareTo(Object o) {
    Console.WriteLine("Derived's CompareTo");

    // This attempt to call the base class's EIM causes infinite recursion
    IComparable c = this;
    c.CompareTo(o);

    return 0;
}
```

In this version, I am casting `this` to an `IComparable` variable, `c`. And then, I use `c` to call `CompareTo`. However, the **Derived**'s public `CompareTo` method serves as the implementation for **Derived**'s `IComparable.CompareTo` method, and therefore, infinite recursion occurs. This could be fixed by declaring the **Derived** class without the **IComparable** interface, like this:

```csharp
internal sealed class Derived : Base /*, IComparable */ { ... }
```

Now the previous `CompareTo` method will call the `CompareTo` method in `Base`. But sometimes you cannot simply remove the interface from the type because you want the derived type to implement an interface method. The best way to fix this is for the base class to provide a virtual method in addition to the interface method that it has chosen to implement explicitly. Then the **Derived** class can override the virtual method. Here is the correct way to define the **Base** and **Derived** classes:

```csharp
internal class Base : IComparable {

    // Explicit Interface Method Implementation
    Int32 IComparable.CompareTo(Object o) {
        Console.WriteLine("Base's IComparable CompareTo");
        return CompareTo(o);    // This now calls the virtual method
    }

    // Virtual method for derived classes (this method could have any name)
    public virtual Int32 CompareTo(Object o) {
        Console.WriteLine("Base's virtual CompareTo");
        return 0;
    }
}

internal sealed class Derived : Base, IComparable {

    // A public method that is also the interface implementation
    public override Int32 CompareTo(Object o) {
        Console.WriteLine("Derived's CompareTo");

        // Now, we can call Base's virtual method
        return base.CompareTo(o);
    }
}
```

Note that I have defined the virtual method above as a public method, but in some cases, you will prefer to make the method protected instead. It is fine to make this method protected instead of public, but that will necessitate other minor changes. This discussion clearly shows you that EIMIs should be used with great care. When many developers first learn about EIMIs, they think that they're cool and they start using them whenever possible. Don't do this! EIMIs are useful in some circumstances, but you should avoid them whenever possible because they make using a type much more difficult.

## Design: Base Class or Interface?

I often hear the question, "Should I design a base type or an interface?" The answer isn't always clear-cut. Here are some guidelines that might help you:

- **IS-A vs. CAN-DO relationship** A type can inherit only one implementation. If the derived type can't claim an IS-A relationship with the base type, don't use a base type; use an interface. Interfaces imply a CAN-DO relationship. If the CAN-DO functionality appears to belong with various object types, use an interface. For example, a type can convert instances of itself to another type (`IConvertible`), a type can serialize an instance of itself (`ISerializable`), etc. Note that value types must be derived from `System.ValueType`, and therefore, they cannot be derived from an arbitrary base class. In this case, you must use a CAN-DO relationship and define an interface.

- **Ease of use** It's generally easier for you as a developer to define a new type derived from a base type than to implement all of the methods of an interface. The base type can provide a lot of functionality, so the derived type probably needs only relatively small modifications to its behavior. If you supply an interface, the new type must implement all of the members.

- **Consistent implementation** No matter how well an interface contract is documented, it's very unlikely that everyone will implement the contract 100 percent correctly. In fact, COM suffers from this very problem, which is why some COM objects work correctly only with Microsoft Office Word or with Windows Internet Explorer. By providing a base type with a good default implementation, you start off using a type that works and is well tested; you can then modify parts that need modification.

- **Versioning** If you add a method to the base type, the derived type inherits the new method, and the user's source code doesn't even have to be recompiled. Adding a new member to an interface forces the inheritor of the interface to change its source code and recompile.

In the FCL, the classes related to streaming data use an implementation inheritance design. The `System.IO.Stream` class is the abstract base class. It provides a bunch of methods, such as `Read` and `Write`. Other classes—`System.IO.FileStream`, `System.IO.MemoryStream`, and `System.Net.Sockets.NetworkStream`—are derived from `Stream`. Microsoft chose an IS-A relationship between each of these three classes and the **Stream** class because it made implementing the concrete classes easier. For example, the derived classes need to implement only synchronous I/O operations; they inherit the ability to perform asynchronous I/O operations from the **Stream** base class.

Admittedly, choosing to use inheritance for the stream classes isn't entirely clear-cut; the **Stream** base class actually provides very little implementation. However, if you consider the Microsoft Windows Forms control classes, in which **Button**, **CheckBox**, **ListBox**, and all of the other controls are derived from **System.Windows.Forms.Control**, it's easy to imagine all of the code that **Control** implements, which the various control classes simply inherit to function correctly.

By contrast, Microsoft designed the FCL collections to be interface-based. The **System.Collections.Generic** namespace defines several collection-related interfaces: **IEnumerable<T>**, **ICollection<T>**, **IList<T>**, and **IDictionary<TKey, TValue>**. Then Microsoft provided a number of classes, such as **List<T>**, **Dictionary<TKey, TValue>**, **Queue<T>**, **Stack<T>**, and so on, that implement combinations of these interfaces. Here the designers chose a CAN-DO relationship between the classes and the interfaces because the implementations of these various collection classes are radically different from one another. In other words, there isn't a lot of sharable code between a **List<T>**, a **Dictionary<TKey, TValue>**, and a **Queue<T>**.

The operations these collection classes offer are, nevertheless, pretty consistent. For example, they all maintain a set of elements that can be enumerated, and they all allow adding and removing of elements. If you have a reference to an object whose type implements the **IList<T>** interface, you can write code to insert elements, remove elements, and search for an element without having to know exactly what type of collection you're working with. This is a very powerful mechanism.

Finally, it should be pointed out that you can actually do both: define an interface and provide a base class that implements the interface. For example, the FCL defines the **IComparer<in T>** interface, and any type can choose to implement this interface. In addition, the FCL provides an abstract base class, **Comparer<T>**, which implements this interface and provides a default implementation for the non-generic **IComparer**'s **Compare** method. Having both an interface definition and a base class offers great flexibility because developers can now choose whichever they prefer.
