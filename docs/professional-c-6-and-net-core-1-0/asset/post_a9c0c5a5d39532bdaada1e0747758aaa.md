
A generic type can implement a generic interface. The same is possible by deriving from a class. A generic class can be derived from a generic base class:

```
public class Base<T>
{
}
```

```
public class Derived<T>: Base<T>
{
}
```

The requirement is that the generic types of the interface must be repeated, or the type of the base class must be specified, as in this case:

```
public class Base<T>
{
}
```

```
public class Derived<T>: Base<string>
{
}
```

This way, the derived class can be a generic or non-generic class. For example, you can define an abstract generic base class that is implemented with a concrete type in the derived class. This enables you to write *generic specialization* for specific types:

```
public abstract class Calc<T>
{
    public abstract T Add(T x, T y);
    public abstract T Sub(T x, T y);
}
```

```
public class IntCalc: Calc<int>
{
    public override int Add(int x, int y) => x + y;
    public override int Sub(int x, int y) => x - y;
}
```

You can also create a partial specialization, such as deriving the `StringQuery` class from `Query` and defining only one of the generic parameters, for example, a `string` for `TResult`. For instantiating the `StringQuery`, you need only to supply the type for `TRequest`:

```
public class Query<TRequest, TResult>
{
}
```

```
public class StringQuery<TRequest> : Query<TRequest, string>
{
}
```

## Static Members

Static members of generic classes are shared with only one instantiation of the class, and they require special attention. Consider the following example, where the class `StaticDemo<T>` contains the static field x:

```
public class StaticDemo<T>
{
    public static int x;
}
```

Because the class `StaticDemo<T>` is used with both a `string` type and an `int` type, two sets of static fields exist:

```
StaticDemo<string>.x = 4;
StaticDemo<int>.x = 5;
WriteLine(StaticDemo<string>.x);    // writes 4
```

## Generic Interfaces

Using generics, you can define interfaces that define methods with generic parameters. In the linked list sample, you’ve already implemented the interface `IEnumerable<out T>`, which defines a `GetEnumerator` method to return `IEnumerator<out T>`. .NET offers a lot of generic interfaces for different scenarios; examples include `IComparable<T>`, `ICollection<T>`, and `IExtensibleObject<T>`. Often older, non-generic versions of the same interface exist; for example, .NET 1.0 had an `IComparable` interface that was based on objects.

`IComparable<in T>` is based on a generic type:

```
public interface IComparable<in T>
{
    int CompareTo(T other);
}
```

> NOTE Don’t be confused by the in and out keywords used with the generic parameter. They are explained soon in the “Covariance and contra-variance” section.

The older, non-generic `IComparable` interface requires an object with the `CompareTo` method. This requires a cast to specific types, such as to the `Person` class for using the `LastName` property:

```
public class Person: IComparable
{
    public int CompareTo(object obj)
    {
        Person other = obj as Person;
        return this.lastname.CompareTo(other.LastName);
    }
    //
```

When implementing the generic version, it is no longer necessary to cast the `object` to a `Person`:

```
public class Person: IComparable<Person>
{
    public int CompareTo(Person other) => LastName.CompareTo(other.LastName);
    //...
```

## Covariance and Contra-variance

Prior to .NET 4, generic interfaces were invariant. .NET 4 added important changes for generic interfaces and generic delegates: covariance and contra-variance. Covariance and contra-variance are used for the conversion of types with arguments and return types. For example, can you pass a `Rectangle` to a method that requests a `Shape`? Let’s get into examples to see the advantages of these extensions.

With .NET, parameter types are covariant. Assume you have the classes `Shape` and `Rectangle`, and `Rectangle` derives from the `Shape` base class. The `Display` method is declared to accept an object of the `Shape` type as its parameter:

```
public void Display(Shape o) { }
```

Now you can pass any object that derives from the `Shape` base class. Because `Rectangle` derives from `Shape`, a `Rectangle` fulfills all the requirements of a `Shape` and the compiler accepts this method call:

```
var r = new Rectangle { Width= 5, Height=2.5 };
Display(r);
```

Return types of methods are contra-variant. When a method returns a `Shape` it is not possible to assign it to a `Rectangle` because a `Shape` is not necessarily always a `Rectangle`; but the opposite is possible. If a method returns a `Rectangle` as the `GetRectangle` method,

```
public Rectangle GetRectangle();
```

the result can be assigned to a `Shape`:

```
Shape s = GetRectangle();
```

Before version 4 of the .NET Framework, this behavior was not possible with generics. Since C# 4, the language is extended to support covariance and contra-variance with generic interfaces and generic delegates. Let’s start by defining a `Shape` base class and a `Rectangle` class (code files `Variance/Shape.cs` and `Rectangle.cs`):

```
public class Shape
{
    public double Width { get; set; }
    public double Height { get; set; }

    public override string ToString() => $"Width: {Width}, Height: {Height}";
}
```

```
public class Rectangle: Shape
{
}
```

### Covariance with Generic Interfaces

A generic interface is covariant if the generic type is annotated with the `out` keyword. This also means that type T is allowed only with return types. The interface IIndex is covariant with type T and returns this type from a read-only indexer (code file Variance/IIndex.cs):

```
public interface IIndex<out T>
{
    T this[int index] { get; }
    int Count { get; }
}
```

The IIndex<T> interface is implemented with the RectangleCollection class. RectangleCollection defines Rectangle for generic type T:

> NOTE If a read-write indexer is used with the IIndex interface, the generic type T is passed to the method and retrieved from the method. This is not possible with covariance; the generic type must be defined as invariant. Defining the type as invariant is done without out and in annotations (code file Variance/RectangleCollection.cs):

```
public class RectangleCollection: IIndex<Rectangle>
{
    private Rectangle[] data = new Rectangle[3]
    {
        new Rectangle { Height=2, Width=5 },
        new Rectangle { Height=3, Width=7 },
        new Rectangle { Height=4.5, Width=2.9 }
    };

    private static RectangleCollection _coll;
    public static RectangleCollection GetRectangles() =>
        _coll ?? (_coll = new RectangleCollection());

    public Rectangle this[int index]
    {
        get
        {
            if (index < 0 || index > data.Length)
                throw new ArgumentOutOfRangeException("index");
            return data[index];
        }
    }

    public int Count => data.Length;
}
```

> NOTE The RectangleCollection.GetRectangles method makes use of the coalescing operator. If the variable `_coll` is null, the right side of the operator is invoked to create a new instance of RectangleCollection and assign it to the variable `_coll`, which is returned from this method afterwards. This operator is explained in detail in Chapter 8.

The RectangleCollection.GetRectangles method returns a RectangleCollection that implements the IIndex<Rectangle> interface, so you can assign the return value to a variable rectangle of the IIndex<Rectangle> type. Because the interface is covariant, it is also possible to assign the returned value to a variable of IIndex<Shape>. Shape does not need anything more than a Rectangle has to offer. Using the shapes variable, the indexer from the interface and the Count property are used within the for loop (code file Variance/Program.cs):

```
public static void Main()
{
    IIndex<Rectangle> rectangles = RectangleCollection.GetRectangles();
    IIndex<Shape> shapes = rectangles;

    for (int i = 0; i < shapes.Count; i++)
    {
        WriteLine(shapes[i]);
    }
}
```

### Contra-Variance with Generic Interfaces

A generic interface is contra-variant if the generic type is annotated with the in keyword. This way, the interface is only allowed to use generic type T as input to its methods (code file Variance/IDisplay.cs):

```
public interface IDisplay<in T>
{
    void Show(T item);
}
```

The ShapeDisplay class implements IDisplay<Shape> and uses a Shape object as an input parameter (code file Variance/ShapeDisplay.cs):

```
public class ShapeDisplay: IDisplay<Shape>
{
    public void Show(Shape s) =>
        WriteLine($"{s.GetType().Name} Width: {s.Width}, Height: {s.Height}");
}
```

Creating a new instance of ShapeDisplay returns IDisplay<Shape>, which is assigned to the shapeDisplay variable. Because IDisplay<T> is contra-variant, it is possible to assign the result to IDisplay<Rectangle>, where Rectangle derives from Shape. This time the methods of the interface define only the generic type as input, and Rectangle fulfills all the requirements of a Shape (code file Variance/Program.cs):

```
public static void Main()
{
    //...
    IDisplay<Shape> shapeDisplay = new ShapeDisplay();
    IDisplay<Rectangle> rectangleDisplay = shapeDisplay;
    rectangleDisplay.Show(rectangles[0]);
}
```

## Generic Structs
