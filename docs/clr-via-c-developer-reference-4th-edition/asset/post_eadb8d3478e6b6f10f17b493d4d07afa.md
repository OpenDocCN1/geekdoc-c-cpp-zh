
Although the CLR allow an interface to define static methods, static fields, constants, and static constructors, a Common Language Specification (CLS)–compliant interface must not have any of these static members because some languages aren't able to define or access them. In fact, C# prevents an interface from defining any of these static members.

In C#, you use the interface keyword to define an interface, giving it a name and its set of instance method signatures. Here are the definitions of a few interfaces defined in the Framework Class Library (FCL).

```c
public interface IDisposable {
  void Dispose();
}
```

```c
public interface IEnumerator {
  Enumerator GetEnumerator();
}
```

```c
public interface IEnumerable<out T> : IEnumerable {
  new IEnumerator<T> GetEnumerator();
}
```

```c
public interface IList<T> : IEnumerable<T>, ICollection {
  void Add(T item);
  void Clear();
  Boolean Contains(T item);
  void CopyTo(T[] array, Int32 arrayIndex);
  void Remove(T item);
  Int32 Count { get; } // Read-only property
  Boolean IsReadOnly { get; } // Read-only property
}
```

To the CLR, an interface definition is just like a type definition. That is, the CLR will define a data structure for the interface type, and reflection can be used to query features of the interface type. Like types, an interface can be defined at file scope or nested within another type. When defining the interface type, you can specify whatever visibility/accessibility (public, protected, internal, etc.) you want.

By convention, interface names are prefixed with an I, making it easy to spot an interface type in source. The CLR does support generic interfaces (as you can see from the previous examples) as well as generic methods in an interface. I will discuss some of the features offered by generic interfaces later in this chapter and in Chapter 12, "Generics," in which I cover generics broadly.

An interface definition can "inherit" other interfaces. However, use the word inherit rather loosely because interface inheritance doesn't work exactly like class inheritance. I prefer to think of interface inheritance as including the contract of other interfaces. For example, the ICollection<T> interface definition includes the contracts of the IEnumerable<T> and IEnumerable interfaces.

This means that:

- Any class that inherits the ICollection<T> interface must implement all of the methods defined by the ICollection<T>, IEnumerable<T>, and IEnumerable interfaces.
- Any code that expects an object whose implements the ICollection<T> interface can assume that the object's type also implements the methods of the IEnumerable<T> and IEnumerable interfaces.

## Inheriting an Interface

In this section, I'll show how to define a type that implements an interface, and then I'll show how to create an instance of this type and use the object to call the interface's methods. C# actually makes this pretty simple, but what happens behind the scenes is a bit more complicated. I'll explain what is happening the scenes later in this chapter.

The System.IComparable<T> interface is defined (in MSCLib.dll) as follows.

```csharp
public interface IComparable<in T> {
    Int32 CompareTo(T other);
}
```

The following code shows how to define a type that implements this interface and also shows that compares two Point objects.

using System;

```csharp
// Point is derived from System.Object and implements IComparable<T> for Point.
public sealed class Point : IComparable<Point> {
    private Int32 m_x, m_y;

    public Point(Int32 x, Int32 y) {
        m_x = x;
        m_y = y;
    }

    // This method implements IComparable<Point>.CompareTo() for Point
    public Int32 CompareTo(Point other) {
        return Math.Sign(Math.Sqrt(m_x * m_x + m_y * m_y) 
            - Math.Sqrt(other.m_x * other.m_x + other.m_y * other.m_y));
    }

    public override string ToString() {
        return String.Format("{0}, {1}", m_x, m_y);
    }
}
```

```csharp
public static class Program {
    public static void Main() {
        Point[] points = new Point[] {
            new Point(3, 3),
            new Point(1, 2),
        };

        // Here a call to Point's IComparable<T> CompareTo method
        if (points[0].CompareTo(points[1]) > 0) {
            Point tempPoint = points[0];
            points[0] = points[1];
            points[1] = tempPoint;
        }
        Console.WriteLine("Points from closest to (0, 0) to farthest:");
        foreach (Point p in points) {
            Console.WriteLine(p);
        }
    }
}
```

The C# compiler requires a method that implements an interface be marked as public. The CLR requires that interface methods be virtual. If you do not explicitly mark the method as virtual in your source code, the compiler marks the method as virtual and sealed; this prevents a derived class from overriding the interface method. If you explicitly mark the method as virtual and unsealed; this allows a derived class to override the interface method.

If an interface method is sealed, a derived class cannot override it. However, a derived class can re-inherit the same interface and can provide its own implementation. When calling an interface method on an object, the implementation associated with the type is called. Here is an example that demonstrates this.

using System;

```csharp
public static class Program {
    public static void Main() {
        **************************** First Example *************
        Base b = new Base();

        // Calls Dispose using b's type: "Base's Dispose"
        b.Dispose();

        // Calls Dispose using b's type: "Base's Dispose"
        ((IDisposable)b).Dispose();

        **************************** Second Example ************
        Derived d = new Derived();

        // Calls Dispose using d's type: "Derived's Dispose"
        d.Dispose();

        // Calls Dispose using d's type: "Derived's Dispose"
        ((IDisposable)d).Dispose();

        **************************** Third Example **********
        b = new Derived();

        // Calls Dispose using b's type: "Base's Dispose"
        b.Dispose();

        // Calls Dispose using b's type: "Derived's Dispose"
        ((IDisposable)b).Dispose();
    }
}

// This class is derived from Object and implements IDisposable
internal class Base : IDisposable {
    // This method is implicitly sealed and cannot be overridden
    public void Dispose() {
        Console.WriteLine("Base's Dispose");
    }
}

// This class is derived from Base and re-implements IDisposable
internal class Derived : Base, IDisposable {
    // This method cannot override Base's Dispose. 'new' is used to indicate
    // that method re-implements IDisposable's Dispose method
    new public void Dispose() {
        Console.WriteLine("Derived's Dispose");
    }

    // NOTE: The next line shows how to call a base class's implementation (if desired)
    // base.Dispose();
}
```

## About Calling Interface Methods

The FCL's System.String inherits System.Object method signatures and their implementations. In addition, the String type also implements several interfaces: IComparable, ICloneable, IConvertible, IEnumerable, IComparable<String>, IEnumerable<Char>, and IEquatable<String>. This means that the String type isn't required to implement (or override) the methods of Object's base type. However, the String type must implement the methods declared in all of the interfaces.

The CLR allows you to define field, parameter, or local variables that are of an interface type a variable of interface type allows you to call methods defined by that interface. In addition, the CLR will allow you to call methods defined by Object because all classes inherit Object's methods. The following code demonstrates this.

```csharp
// The s variable refers to a String object.
String s = "Jeffrey";
// Using s, I can call any method defined in
// String, Object, IComparable, ICloneable, IConvertible, IEnumerable, etc.

// The cloneable variable refers to the same String object
Cloneable cloneable = s;
```

300 PART II Designing Types **
