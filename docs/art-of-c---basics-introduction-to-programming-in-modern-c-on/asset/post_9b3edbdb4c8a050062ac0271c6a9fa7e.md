
![](img/25af69ec45b3c0b589a8dccd0c2a88be_325_0.png)

## 20.2. Code Review

A "point" is a fundamental concept. Just like a number.

We live in a three-dimensional space, and we often deal with (conceptually) two-dimensional surfaces like a notepad, a map, a computer screen, etc. Let’s try representing a point in a 2-D space as a pair of numbers.

Traditionally, we would have most likely used `struct` to define a type for "points" in C#. Here’s a definition of `SPoint`.

*euclid-distance/SPoint.cs (lines 3-41)*

```csharp
public readonly struct SPoint : IPoint, IEquatable<SPoint>,
    IComparable<SPoint> {
  public float X { get; init; }
  public float Y { get; init; }

  public SPoint(float x, float y) => (X, Y) = (x, y);

  public float Radius() => (float)Math.Sqrt(X * X + Y * Y);

  public override string ToString() => $"({X},{Y})";

  public override bool Equals(object? obj) =>
    obj is SPoint point && X == point.X && Y == point.Y;

  public override int GetHashCode() => HashCode.Combine(X, Y);

  public bool Equals(SPoint other) => X == other.X && Y == other.Y;

  public static bool operator ==(SPoint left, SPoint right) =>
    left.Equals(right);

  public static bool operator !=(SPoint left, SPoint right) =>
    !(left == right);

  public int CompareTo(IPoint? other) => other is SPoint sp ?
    CompareTo(sp) : 1;

  public int CompareTo(SPoint other) => (Radius() - other.Radius())
    switch {
      < 0 => -1,
      > 0 => 1,
      _ => 0,
    };

  public static bool operator >(SPoint left, SPoint right) =>
    left.Radius() > right.Radius();

  public static bool operator <(SPoint left, SPoint right) =>
    left.Radius() < right.Radius();

  public static bool operator >=(SPoint left, SPoint right) =>
    left.Radius() >= right.Radius();

  public static bool operator <=(SPoint left, SPoint right) =>
    left.Radius() <= right.Radius();

  public IPoint Copy() => Copy((0, 0));

  public IPoint Copy((float, float) delta) => new SPoint(X +
    delta.Item1, Y + delta.Item2);

  public void Deconstruct(out float X, out float Y) => (X, Y) =
    (this.X, this.Y);
}
```

Here's an alternative type definition, `RPoint`, using `record class` for representing points in a two dimensional space.

*euclid-distance/RPoint.cs (lines 3-21)*

```csharp
public record RPoint(float X, float Y) : IPoint, IComparable<RPoint> {
  public float Radius() => (float)Math.Sqrt(X * X + Y * Y);

  public int CompareTo(IPoint? other) => other is RPoint rp ?
    CompareTo(rp) : 1;

  public int CompareTo(RPoint? other) => other is null ? 1 :
    (Radius() - other.Radius()) switch {
      < 0 => -1,
      > 0 => 1,
      _ => 0,
    };

  public static bool operator >(RPoint left, RPoint right) =>
    left.Radius() > right.Radius();

  public static bool operator <(RPoint left, RPoint right) =>
    left.Radius() < right.Radius();

  public static bool operator >=(RPoint left, RPoint right) =>
    left.Radius() >= right.Radius();

  public static bool operator <=(RPoint left, RPoint right) =>
    left.Radius() <= right.Radius();

  public IPoint Copy() => Copy((0, 0));

  public IPoint Copy((float, float) delta) =>
    new RPoint(X + delta.Item1, Y + delta.Item2);
}
```

In fact, the (abstract) notion of a "point" can be encapsulated as follows, using `interface`. An interface in C# defines a set of "behaviors", but not "data".

*euclid-distance/IPoint.cs (lines 3-13)*

```csharp
public interface IPoint : IComparable<IPoint> {
  float X { get; }
  float Y { get; }

  float Radius();

  IPoint Copy();
  IPoint Copy((float, float) delta);

  void Deconstruct(out float X, out float Y);
}
```

The prefix `I` (for *Interface*) is conventional, and it is not required. This prefix is often used when we define both interface and concrete type, and the `I` prefix can be useful to distinguish the interfaces from other concrete types.

One thing to notice from the definition of *IPoint* is the property declarations. For example,

```csharp
float X { get; }
```

This declares a (readonly) property `X` of type *float* in an interface. As you may recall from the earlier lessons, the exactly same syntax is used in the "auto property" declaration in a class or struct (or, their record counterparts). This can be a cause of confusion for some people who are new to C#.

This syntax in an interface does not define an auto property since the interfaces cannot have data/fields. It is an implicit "abstract property". Any (non-abstract) class that implements this interface will need to implement this property.

Using this new type *IPoint*, we can provide an implementation for more than one types, namely, for both *SPoint* and *RPoint*.

## 20.2. Code Review

The following function, or static method, computes a Euclidean distance between two points, and it can be used for both SPoint and RPoint.

*euclid-distance/Distance.cs (lines 4-5)*

```csharp
public static float Distance(IPoint p1, IPoint p2) =>
  (float)Math.Sqrt((p1.X - p2.X) * (p1.X - p2.X) +
    (p1.Y - p2.Y) * (p1.Y - p2.Y));
```

Here’s a method to sort an array of points, implemented generically for IPoint.

*euclid-distance/Bubble.cs (lines 3-25)*

```csharp
static class Bubble {
  internal static void Sort<T>(IList<T> arr) where T : IPoint {
    for (var i = 0; i < arr.Count - 1; i++) {
      for (var j = 0; j < arr.Count - i - 1; j++) {
        if (Compare(arr[j], arr[j + 1]) > 0) {
          (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
        }
      }
    }
  }

  private static int Compare<T>(T l, T r) where T : IPoint {
    var (dl, dr) = (l.Radius(), r.Radius());
    return (dl - dr) switch {
      < 0 => -1,
      > 0 => 1,
      _ => 0,
    };
  }

  internal static void Print<T>(this IEnumerable<T> arr) =>
    Console.WriteLine($"{{{string.Join(", ", arr)}}}");
}
```

## 20.3. Pair Programming - Interfaces, Polymorphism, Custom Tuple Deconstruction

An interface is a reference type. The C# keyword `interface` is used to define a reference type.

Unlike the types defined by `struct` and `class`, an `interface` type is always an "abstract type". It defines a set of "behaviors", and it can provide some default implementations, but the objects of an interface type cannot be directly instantiated. Interfaces do not include "states" or "data". They only prescribe "behaviors".

Interfaces provide "polymorphic behavior" to other types. Types defined with `class`/`record` and `struct`/`record struct` can inherit behaviors from interfaces, e.g., by "implementing the interfaces".

C# also provides another way to define a type which is primarily behavior, namely `abstract class`. An abstract class defines a type that cannot be directly instantiated like `interface`. But, it can still include states unlike the `interface`. We will see example uses of abstract `class` in later lessons.

The `IPoint` public interface of the sample program defines a set of behaviors, i.e., properties and methods, that encapsulate the abstract concept of the "point" in the 2-D space.

That is, a point comprises two numbers (e.g., `float` in this example) and they are publicly accessible (e.g., through properties named `X` and `Y`).

```csharp
float X { get; }
float Y { get; }
```

Given a point, one can obtain a certain number called the "radius" of the point.

```csharp
float Radius();
```

In C#, properties and methods are more or less equivalent to each other despite their syntactic differences. The "methods" that (directly) access "data" are typically implemented via readonly or read-write properties. The `Radius()` method in this example could have been declared as a readonly property. In fact, that could have been more appropriate since the concept of the "radius" of a point is really "data".

In many cases, it is just a matter of style or preference. One thing to note, however, is that the methods in an interface can have default implementations. On the other hand, the properties in an interface are always abstract.

Points can be "copied", either at the same location or at a new location displaced by "delta":

```csharp
IPoint Copy();
IPoint Copy((float, float) delta);
```

And, they can be "deconstructed" into a tuple of two `float` numbers.

```csharp
void Deconstruct(out float X, out float Y);
```

In fact, we could have even provided its default implementation for all types that inherit the behaviors of this interface. For instance,
