
element traversal order) using b.Equals(a), things will likely go terribly wrong. And typically with such problems, the issue will crop up only after the code has run a long time.

### Overloading the == Operator

Finally, after some mandatory detours through the world of System.Object's methods, we've arrived at our final goal of overloading the == operator. Doing so is encouraged if the type carries value semantics, meaning two instances are really the same. A good example is a complex number type, which may be implemented as a class or a struct. If no value semantics are present, it's best to omit a == operator definition in favor of just an Equals override (if needed).

One first thing to realize is that no default == operator is present for types, in contrast to the availability of a default Equals implementation. For example, the following won't work:

```csharp
struct Point { public int X; public int Y; }
...
var p = new Point { X = 1, Y = 2 };
var q = p;

Console.WriteLine(p == q);  // Fails since no == operator is found.
```

For classes, things are a bit different because the use of a == operator will be allowed, as shown here. However, there's no default type-specific implementation for == as there is for Equals. Instead, == applied to any two reference-typed objects will return the result of a reference-equality check:

```csharp
class Person { public string Name; public int Age; }
...
var p = new Person { Name = "Bart", Age = 27 };
var q = p;

Console.WriteLine(p == q);  // Returns true due to reference equality.
```

Following the guidelines, we won't overload == for our Person class because you can barely claim a person to be a value. In that case, just overriding Equals suffices. For value types, though, if you override Equals, you must also implement an == operator:

```csharp
struct Point
{
    private readonly int _x, _y;

    public Point(int x, int y)
    {
        _x = x; _y = y;
    }

    public override bool Equals(object obj)
    {
        if (obj == null || obj.GetType() != this.GetType())
            return false;

        var other = (Point)obj;
        return this == other;
    }

    public override int GetHashCode()
    {
        return _x.GetHashCode() ^ _y.GetHashCode();
    }

    public static bool operator ==(Point p1, Point p2)
    {
        return p1._x == p2._x && p1._y == p2._y;
    }

    public static bool operator !=(Point p1, Point p2)
    {
        return !(p1 == p2);
    }
}
```

Notice how we avoided any redundancy in equality checking code by calling into our operator overload from the Equals method. Also, the mandatory paired != operator uses the == implementation to determine its result.

Make sure to test all uses to catch any possible cyclic reference that causes some infinite recursion. It's an easy trap to fall into. For the preceding code, the next series of tests do a decent job at checking some properties:

```csharp
var p1 = new Point(1, 2);
var p2 = new Point(2, 3);
var p3 = new Point(1, 2);
var s = "Other";

// False
Console.WriteLine(p1.Equals(p2));          Console.WriteLine(p2.Equals(p1));
Console.WriteLine(p1 == p2);               Console.WriteLine(p2 == p1);
Console.WriteLine(p1.Equals(s));           Console.WriteLine(s.Equals(p1));
Console.WriteLine(p1.Equals(null));  // Console.WriteLine(null.Equals(p1));

// Shouldn't compile as there's no == operator between Point and string
//Console.WriteLine(p1 == s);               Console.WriteLine(s == p1);

// True
Console.WriteLine(p1.Equals(p3));      Console.WriteLine(p3.Equals(p1));
Console.WriteLine(p1 == p3);            Console.WriteLine(p3 == p1);
```

Based on our discussion about both of Object's Equals methods and the discussion about == operator overloading, none of the results shown earlier should come as a surprise.

### STRING INTERNING AND EQUALITY

Strings are interesting objects for a number of reasons. They're immutable, are implemented as reference types, but have value semantics. Adding all of those properties together, we have something rather exotic. Matters get even fancier since the runtime knows a great deal about string objects. One thing it does is so-called interning, allowing strings with the same contents to be reused, which is possible thanks to immutability. The following code shows some of this behavior:

```csharp
var s1 = "Hello";
var s2 = "Hel"; s2 += "lo";  // Runtime concatenation to avoid compiler smarts
var s3 = string.Intern(s2);    // Memory used for s1 will be found to equal s2
Console.WriteLine(s1 == s2);   // Value equality on string contents -> true
Console.WriteLine(s1 == s3);   // Same deal
Console.WriteLine(s1.Equals(s2)); // Value equality again
Console.WriteLine(s1.Equals(s3)); // Same deal
Console.WriteLine(Object.ReferenceEquals(s1, s2)); // Not the same!
Console.WriteLine(Object.ReferenceEquals(s1, s3)); // But those are...
```

The second-to-last call returns false because s1 and s2 are different references; however, using interning s3 will have the same reference as s1.

### How Operators Are Translated

To conclude our discussion about user-defined operators, we take a quick peek at the way their definition gets implemented. As revealed by the static modifier, operators are associated with the type on which they're defined, rather than with an instance. This has some advantages in terms of compile-time resolution of operators but also limits their expressiveness in terms of runtime dynamism. It's also not possible to create interfaces that require an implementing type to support certain operators, which is precisely what the mythical INumeric interface would be about ("can Add, Multiply, and so on"). This is a bit of an unfortunate implication of the design of operators.

Operators' operational nature makes their most natural implementation to be regular (static) methods. No metadata is associated with them to declare their "operatorness." Instead, a simple naming convention was introduced such that languages that support user-defined operators can search for them. In particular, each operator has an English noun (such as Equality for ==). An op_ prefix indicates the method is an operator. Some languages that don't support direct use of operators in terms of syntax can still make operators available as regular method calls. Language documentation on MSDN provides those names for all supported operators, in case you're interested.

to one with a larger range (but including the first's range entirely). The preceding example of int to long falls under this category because every int can be held by a long, too. Such widening conversions can be done implicitly, whereas the narrowing ones (that may lose information or fail at runtime) must usually be carried out explicitly.

Back to the world of C#, one of the explicit conversion examples is exactly the opposite of the one shown earlier. Instead of going from an int to a long, we could try exactly the other way around. In that case, the compiler won't allow you to do this implicitly because the conversion may lose information. Not every 64-bit long fits in a 32-bit int:

```csharp
long l = 123;
int i = (int)l; // Dear compiler: believe me, I know what I'm doing!
```

Recall from our coverage of expressions that the checked keyword can be used to turn on overflow checking as part of an expression's evaluation. This can be used for such explicit conversions, too, triggering an OverflowException if the conversion fails. The following will actually do so:

```csharp
long l = 2L << 32; // Notice the use of L to calculate 2^32 as a long
int i = checked((int)l); // This will throw an OverflowException.
```

### Enumeration Conversions

As you learned in Chapter 11, "Fields, Properties, and Indexers," enumerations are nothing but numeric value types in disguise. The underlying type is what determines all of an enum's values' representation. Only one implicit conversion exists, from the literal 0 to a value of the enum's type. This allows default-value initialization of enum values. It's assumed that the zero value of an enum provides a meaningful default. Often, it is named None for precisely that reason:

```csharp
ConsoleColor color = 0; // Will be the same as ConsoleColor.Black.
FileShare share = 0; // Will be the same as FileShare.None.
FileMode mode = 0; // Meaningless, since there's no 0 value in the enum.
```

Explicit conversions requiring a cast exist between the enum type and its underlying type (but in fact also to other numeric types), in both directions:

```csharp
ConsoleColor red = (ConsoleColor)12;
int twelve = (int)red;
```

### Nullable Conversions

Intended to be a natural extension to the use of regular value types, their nullable forms support a series of conversions that are much expected. For example, you can always go
