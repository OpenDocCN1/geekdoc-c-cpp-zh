
These operator definitions make handling equality and comparisons much more natural for LogEntry instances.

## Nonstandard Operator Behavior

Occasionally, arithmetic operators are useful beyond truly arithmetic operations. For example, string instances can be “added” together, and most programmers understand that adding two strings concatenates them, so "key" + "board" becomes "keyboard". In arithmetic, addition is commutative, so a + b gives the same result as b + a. This clearly isn’t true when used with string instances, but concatenating two strings with + is a widely used and accepted convention.

When we bend the rules this way, it’s especially important that we’re mindful of conventions, natural usage, and expectations. For instance, in arithmetic the ability to add numbers together goes hand in hand with the facility for subtraction. Consider what subtracting one string from another might mean. Would it remove all instances of the right-hand argument from the left-hand string? Only if it appeared at the end of the string? String subtraction doesn’t have the natural and conventional appeal that string addition/concatenation does.

We’d normally expect to find a symmetry between + and -, and symmetry is usually a desirable quality. When we overload ==, the compiler insists that we also implement the != operator. Coupling addition with subtraction for string values is one example where symmetry is undesirable, because it introduces conflicting expectations.

Symmetry is inappropriate in other situations too. For example, matching every property get accessor with a corresponding set is superficially attractive but contradicts the recommendation that value types are immutable. This is another instance where we need to apply our own judgment on whether symmetry is a positive characteristic.

## Summary

> It's not hard to make decisions when you know what your values are.
> —Roy Disney, American film writer and producer

Although C# has its own definition of ValueType, the broader concept of a value isn’t specific to C#. That more general idea of a value type has commonalities with the C# definition, but notable differences exist.

The language definition of a value type focuses mainly on the memory requirements and behavior associated with structs. We need to take other factors into account, however, in order to decide when and how to introduce values into our programs. In this chapter, we’ve explored some of those considerations by contrasting values with reference types—in particular, by examining how values fulfill specific and important roles in a program.

Object-oriented systems are made up of several kinds of objects with varying emphasis on the characteristics of identity, state, and behavior.

When an object’s role places a high importance on instance identity, it’s a strong indicator that the type shouldn’t be a value type. When the priority is an object’s state and identity is unimportant, the type is almost certainly best modeled as a value.

Whether a type has a single field or many fields isn’t necessarily the best metric for choosing whether to make it a value. Sometimes we want value semantics, and sometimes reference semantics are more important. The phrases *value semantics* and *copy by value* are sometimes used interchangeably and even defined in terms of each other. However, value semantics has more to do with value-based equality than with copying.

Distinguishing value types from other kinds of types is an important first step in partitioning their responsibilities in an application. Identifying candidate value types helps us clarify our designs by introducing specialized types that encapsulate behavior and responsibilities. In turn, we benefit from a more modular system, both in its implementation and in the testing it requires. Having decided a type should be modeled as a value, we have more options for implementing it. C# has rich support for all user-defined types, but its facilities for value types are sometimes unappreciated.

## 7

## VALUE TYPES AND POLYMORPHISM

![](img/47f0004b0ac0322f285ca59a19bca333_236_0.png)

As an object-oriented programming (OOP) language, C# has good support for features that allow us to capture complex ideas and express them intuitively, such as classes, virtual methods, and inheritance. However, the language support for inheritance doesn’t extend to value types. Structs and record structs implicitly derive from the ValueType class, which is derived directly from object, but they can’t inherit any other type and can’t themselves be inherited; that is, structs and record structs are implicitly sealed. Inheritance is a central feature of OOP that enables us to treat a reference to a derived class as though it refers to the base class, overriding the base class’s properties and methods to have new behavior as needed. These features don’t apply to value types, but that doesn’t mean value types are inferior.

Using the term polymorphism interchangeably with inheritance is common, but polymorphism is a more general concept; it relates to writing

code that works uniformly for a variety of types to reduce duplication. As this chapter discusses, inheritance is just one kind of polymorphism, and while there are sound technical and semantic reasons for why value types can’t employ inheritance relationships, they can take advantage of other kinds of polymorphism.

We’ll explore the following:

- Why value types are sealed and why value-like types in general shouldn’t use inheritance
- How subtyping differs from subclassing and why it matters
- What *type substitutability* means and how it relates to inheritance
- Where to use other kinds of polymorphism, rather than inheritance, to model relationships between objects

## Why Value Types Are Sealed

The principal technical reason for prohibiting inheritance for structs, and by extension record structs, is that they have different lifetime and storage characteristics than reference types. The restriction is more than an arbitrary rule: it results directly from how value type variables behave in memory, and how that behavior differs from reference types.

Inheritance between classes allows us to use a reference to a base class type to refer to an instance of a derived class, so the static, compile-time type of a reference variable isn’t necessarily the same as the dynamic, run-time instance type. This characteristic permits *virtual dispatch* for method calls—the mechanism whereby the appropriate method implementation will be called based on the actual type of the object at run time—and relies on the extra level of indirection afforded by references; therefore, inheritance is appropriate only for reference types.

Value type variables directly contain their data, so we can’t declare a variable as one type to represent an instance of a different type, other than via boxing. Inheriting from a struct thus makes no sense, and the compiler forbids it.

Remember, though, that we can use classes to model value-like behavior. As you saw in Chapter 6, string behaves like a value but is implemented as a reference type. The string type uses a value-based (rather than identity-based) equality comparison, is immutable, and has various other characteristics that identify it as a value. Being a class, string could support virtual method dispatch, but we can’t derive from the string class because it’s explicitly sealed. This means we can’t create our own augmented subclass of string any more than we could inherit from DateTime, Guid, or any other value type.

Like the string class, records are reference types but have value-like equality behavior. Records can derive from other records and can also have virtual methods, so they seemingly unify the ideas of values and

inheritance. However, using records is not that straightforward. We need to note the subtleties and avoid the pitfalls when using any inheritance, whether between classes or records.

When we allow our types to participate in inheritance relationships, we need to be mindful of what deriving from those types might entail. There’s a difference between implementation and interface inheritance. Inheriting an implementation presents some of the same difficulties as deriving from a value type. To explore why doing so is ill-advised, let’s look at a class with value-like characteristics and use implementation inheritance to demonstrate some of the problems that can result.

## Implementation Inheritance

Anytime we inherit from a concrete class—that is, one that’s not fully abstract—we are, by definition, inheriting its implementation. Listing 7-1 shows a simple inheritance relationship: a TranslucentColor class derives from a Color base class and adds a new feature of its own.

```
public class Color
{
    public Color(int red, int green, int blue)
        => (Red, Green, Blue) = (red, green, blue);

    public int Red  { get; }
    public int Green { get; }
    public int Blue  { get; }
}

public class TranslucentColor : Color
{
    public TranslucentColor(int red, int green, int blue, int alpha)
        : base(red, green, blue) => Alpha = alpha;

    public int Alpha { get; }
}
```

Listing 7-1: Creating a derived class, TranslucentColor, that inherits the implementation of Color

This TranslucentColor class subclasses the Color class and inherits all of Color’s structural representation, along with its methods and properties. Both classes have automatic properties, which are each given a backing field of the same type as the property—int in this example—and every field of Color is inherited by TranslucentColor.

Even if we’d used private fields in Color and returned their values via the properties, those fields would be inherited by the TranslucentColor class, although they’d still be accessible only via the inherited public properties.

The implementation inherited by TranslucentColor from Color depends on those private fields. An instance of TranslucentColor requires its own
