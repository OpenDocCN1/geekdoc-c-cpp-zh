
## VALUE AND REFERENCE TYPES

![](img/47f0004b0ac0322f285ca59a19bca333_56_0.png)

We can create new types in C# in several ways, and we need to consider the individual characteristics of each approach to determine which best suits our goals. In particular, knowing how value types differ from reference types helps us choose the right way forward, because these differences have significant and sometimes unconsidered implications when we’re defining our own types. Certain trade-offs will affect how we design our type and what we can use it for. In this chapter, we’ll investigate those differences and what they mean for our programs.

We’ll explore the following:

- What choices we have when creating our own types
- Why C# has both reference types and value types
- How choosing one or the other affects construction, null checking, and other type behavior
- Why value type is not the same as value semantics
- Where different types are stored in memory and how that affects an object's lifetime

## User-Defined Types

Most modern programming languages allow you to create custom types. The basic principles of user-defined types in C# will be familiar to programmers of many other languages, but some of the details are different. Therefore, in this section we’ll examine the four kinds of user-defined types: structs, classes, and the newer records and record structs (introduced in C# v9.0 and v10.0, respectively).

It’s important to recognize that the behavior of these types relies heavily on whether they are reference types or value types. Let’s look briefly at each kind of user-defined type with these differences in mind.

### Structs and Classes

Listing 2-1 defines a simple struct to represent colors.

```
public readonly struct Color
{
    public Color(int r, int g, int b)
        => (Red, Green, Blue) = (r, g, b);

    public int Red { get; }
    public int Green { get; }
    public int Blue { get; }
}
```

Listing 2-1: Defining a simple struct

The Color struct is marked readonly to indicate that instances of Color are immutable—that is, they never change their value. Correspondingly, none of the three properties (Red, Green, and Blue) has a set accessor, so their values can’t be changed after they’ve been given initial values using the constructor.

The constructor in this example uses the expression body syntax (=>), which you saw in Chapter 1, instead of a body enclosed between braces {...}. We make the expression body a single-line statement by using tuple assignment, which assigns the tuple of three parameter values r, g, and b to the tuple of three properties. The compiler translates this syntax into an efficient assignment from the parameter values directly to the respective backing fields for the Red, Green, and Blue properties.

The readonly keyword in the struct’s definition is not mandatory but reinforces that instances of Color are immutable. Immutable value types

make our code easier to comprehend and may allow some optimizations by the compiler.

By contrast, if we define a Color class instead of a struct, we can't use the readonly keyword in its definition, although we can make it immutable by not providing set accessors for the properties. The only other difference in defining Color as a class is the use of the class keyword in the definition:

```
public class Color
{
--snip--
```

The definition of Color is otherwise identical to that in Listing 2-1.

The principal difference between these two types is that a class is a reference type, and a struct is a value type. Before we analyze the implications of this difference, let's look at record and record struct types.

### Records and Record Structs

As of C# v9.0, we can define a record type with the record keyword. Records introduce a new syntax for compactly defining a type. Listing 2-2 creates a record type named Color.

```
public record Color(int Red, int Green, int Blue);
```

Listing 2-2: Defining a record

This example shows a positional record; the Color type has no body, but the type definition has its own positional parameters that are used by the compiler to generate a complete type. Behind the scenes, the compiler translates the record into a class definition, meaning that records are reference types. The compiler also translates the parameter names Red, Green, and Blue into public properties of the same name, along with a public constructor with matching parameters to initialize the property values. The positional parameters are also used by the compiler to generate other methods, including Equals, GetHashCode, and ToString, which are overrides of their counterparts in the object base class.

Listing 2-3 creates a new instance of the Color record and uses its properties exactly as if it were a class or a struct.

```
var tomato = new Color(Red: 255, Green: 99, Blue: 71);

Assert.That(tomato.Red, Is.EqualTo(255));
Assert.That(tomato.Green, Is.EqualTo(99));
Assert.That(tomato.Blue, Is.EqualTo(71));
```

Listing 2-3: Creating an instance of Color

Here, we use named arguments when constructing the tomato variable of type Color to emphasize the names given by the compiler to the constructor parameters. Note that the property names used in the assertions are

identical to the names used in the constructor, and that both match the names used in the record definition.

> **NOTE**  
> *One important difference between records and structs or classes relates to handling equality comparisons between two instances, a topic we’ll examine in more detail in “Identity Equality vs. Value Equality” on page 47.*

Very closely related to records are record structs, introduced in C# v10.0. In contrast to records, which are compiled as classes, record structs are translated by the compiler into struct definitions, making them value types. Otherwise, they’re the same as records. Record structs are denoted by the record struct keywords, as shown here:

```
```csharp
public readonly record struct Color(int Red, int Green, int Blue);
```
```

This record struct, much like the struct in Listing 2-1, is marked readonly. If we left out the readonly keyword, the properties generated by the compiler would be read-write properties, with both get and set accessors. Using the readonly keyword makes Color an immutable record struct.

### Inheritance

One common way of representing relationships between classes and between records is to use *inheritance*, or deriving one type from another. However, we can’t apply inheritance to structs or record structs; it’s available only to reference types.

Another restriction of inheritance is that a record can inherit from another record but not explicitly from a class. Similarly, classes can’t inherit from records. In every other respect, records follow the same rules and have the same characteristics as classes as far as inheritance is concerned. Classes and records can define virtual methods and properties, allowing a more derived type to provide its own behavior by overriding the method or property, and we can choose to ignore, override, or hide any virtual methods in a derived type.

In contrast, structs and record structs are implicitly *sealed*, meaning that inheriting from them is prohibited. If we attempt to derive from a struct or record struct, we get a compile-time error. Structs and record structs can’t inherit from another user-defined type either.

Another restriction for a class or record is that it can inherit from only one base type. Any attempt at multiple inheritance results in a compiler error. If no base type is explicitly specified, object becomes the implied base class. As you’ll see in “The Common Type System” on page 45, every type ultimately inherits from object, either directly or indirectly. For example, the Command class in Listing 2-4 implicitly derives from object, while the DummyCommand class derives explicitly from Command, implicitly inheriting from object via the Command base class.
