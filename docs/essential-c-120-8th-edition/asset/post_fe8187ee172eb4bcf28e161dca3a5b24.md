
# Reference Equality versus Value Equality

Before we consider examples, however, let's consider why we need to implement value-based equality (or value equality for short) in the first place. Two references are identical (reference equal) if both refer to the same instance of object. On the other hand, objects that have the same values are value equal. And, to support value equal, a type needs to implement value-based equality. Two objects that are reference equal are also value equal—the comparison is between two references to the same object. However, two objects can be of equal value if the (relevant) data between them is also equal. Only reference types can be reference equal, thereby supporting the concept of identity—the two references refer to the same instance.

In contrast, value types can never be reference equal. If you compare 42 is reference equal to 42, the answer is always false. Each value type is stored in a different location (reference) in memory, and even the simple act of passing value types to method for comparison will create additional copies of the value types.

```
Calling ReferenceEquals() on value types will always return false.
```

While value types can never be reference equal, a reference type can support value equals. object includes a static method called ReferenceEquals() that checks whether the two arguments are identical—reference equal. In addition, object defines a virtual Equals() method that, by default, relies on ReferenceEquals() for reference types. However, this Equals() method can be customized (on both reference types and value types) so that they implement value equality rather than reference.

In fact, you should always override Equals() on value types because otherwise you would be left with the default implementation that compares only the first field for value equality. This, however, is insufficient. If a value type had three properties, for example, then checking for value equality by comparing only the first one would likely be inadequate. For example, given an Angle object, a comparison of the first property (Degrees) is not adequate. Two Angles are equal only if Degrees,

# Chapter 9: Introducing Structs and Records

Minutes, and Seconds are equal (and potentially any other properties that the Angle includes). Therefore, it is almost always necessary to provide a custom implementation of value equality on a value type.

Value equality is not limited to value types, however. Value type equality might also make sense on a reference type. string is a great example. Although string is a reference type, the comparison of two strings should be equal if all the letters in the string are identical, even if the two strings are different instances.

In addition, a correct override of Equals() requires a host of additional members to exist and potentially be overridden, described later in the section “Implementing Value Equality” (https://essentialsharp.com/implementing-value-equality). These include GetHashCode() and the == and != operators. Before then, let's delve into what a value type is.

> NOTE The implementation of object.Equals(), the default implementation on all objects before overriding, relies on ReferenceEquals() alone. All value types override the default implementation to instead compare one or more values within the value type. Reference types can optionally also override Equals() to support value equality. It is always necessary to implement equality on custom value types.

# Structs

The C# built-in types, such as bool and int, are value types, except for string and object, which are reference types. Numerous additional value types are provided within the framework. Developers can also define their own value types.

To define a custom value type, you use a syntax similar to the syntax you would use to define class and interface types. The key difference in the syntax is that value types use the keyword struct (Listing 9.1).

Unfortunately, the commented-out ellipses represent a host of complexity as we will come to see later in the chapter.

# LISTING 9.1: Example struct

```c
public struct Angle
{
    // ...
}
```

# Declaring a Record Struct

Fortunately, starting with C# 9.0, a lot of the complexity associated with creating a struct is eliminated with a new contextual keyword—record—that triggers compiler it generating much of the important and complex code related to value type behavior. Learning 9.2 provides an example. With this simple syntax, we have a value type that describes a high-precision angle in terms of degrees, minutes, and seconds. (A *minute* is one-sixtieth of a degree, and a *second* is one-sixteenth of a minute.) This system is used in navigation because it has the nice property that an arc of one minute over the surface of the ocean at the equator is exactly one nautical mile.

# LISTING 9.2: Declaring a struct

```c
// Use the record struct constructor to declare a value type
public readonly record struct Angle(
    int Degrees, int Minutes, string? Name = null);
```

The syntax, which uses a primary constructor, is all that is needed to define the entire type. Unlike regular primary constructors explained in Chapter 6 (and not available until C# 12.0), however, a record’s primary constructor also generates an initial set of properties from the properties (the optional¹) positional parameters. As a result, this simple code construct, called a **record struct**, has all the requisites that you need to build a value type including value declaration, data storage with properties, immutability, constructor initialization, deconstruction, equivalence behavior, and even toString() diagnostic capabilities.

+ 1. Both the positional parameters and the parentheses surrounding them (when there are no positional parameters) are optional. Although it would be peculiar to declare with only parenthesis, as doing so would be similar to declaring an empty struct or class.

# Chapter 9: Introducing Structs and Records

You will notice the Listing 9.2 that there is both a generated constructor and a deconstructor based solely on the positional parameters. This is in addition to the properties (not shown) defined for the same. Also, two instances of the Angle are evaluated as equal if the properties are equivalent, an equivalence implemented according to the guidelines for overriding the equality operator.

LISTING 9.3: Working with the Record Struct

```c
using System;
using System.Diagnostics;

public class Program
{
    public static void Main()
    {
        // The constructor is generated using positional parameters
        (int degrees, minutes, seconds) = (90, 0, 0);
        Angle angle = new(degrees, minutes, seconds);

        // Records include ToString() implementation
        // that returns: "Angle = 90, Minutes = 0, Seconds = 0"
        Console.WriteLine(angle.ToString());

        // Records has a deconstructor using positional parameters
        if (angle is (int, int, int) angleData)
        {
            Trace.Assert(angle.Degrees == angleData.Degrees);
            Trace.Assert(angle.Minutes == angleData.Minutes);
            Trace.Assert(angle.Seconds == angleData.Seconds);
        }

        Angle copy = new(degrees, minutes, seconds);
        // Records provides a custom equality operator.
        Trace.Assert(angle == copy);

        // The with operator has object initializer
        // syntax for instantiating a modified copy.
        copy = angle with {};
        Trace.Assert(angle == copy);

        Angle modifiedCopy = angle with { Degrees = 180 };
        Trace.Assert(angle != modifiedCopy);
    }
}
```

# Record Struct Code Generation

All the functionality of a record struct is generated by the C# compiler at compile time. The C# equivalent of the generated code appears in Listing 9.4.

Listing 9.4: Equivalent Record Struct Generated C# Code

```csharp
using System;
using System.Runtime.CompilerServices;
using System.Text;

[CompilerGenerated]
public readonly struct Angle : IEquatable<Angle>
{
    public int Degrees { get; init; }
    public int Minutes { get; init; }
    public int Seconds { get; init; }
    public string? Name { get; init; }
    public Angle(int Degrees, int Minutes, int Seconds, string? Name)
    {
        this.Degrees = Degrees;
        this.Minutes = Minutes;
        this.Seconds = Seconds;
        this.Name = Name;
    }

    public override string ToString()
    {
        StringBuilder stringBuilder = new();
        stringBuilder.Append("Angle");
        stringBuilder.Append("{ ");
        if (PrintMembers(stringBuilder))
        {
            stringBuilder.Append('\'');
        }
        stringBuilder.Append("}");
        return stringBuilder.ToString();
    }
}
```
