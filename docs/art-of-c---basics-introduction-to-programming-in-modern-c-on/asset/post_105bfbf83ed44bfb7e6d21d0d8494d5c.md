
It should be noted that the base type `Employee` includes neither `Manage()` nor `Work()` methods. Only an object of the `Manager` type can use the method `Manage()` and only an object of the `Worker` type can use the method `Work()`. That is, `managerOrg1[0].Manage()` or `managerOrg1[0].Work()` would have led to a compile error at build time.

This syntax saves us from the need to do an explicit casting after the `is` testing.

In the case of the `as` expressions, we can do something like this:

```csharp
Console.WriteLine($"{(managerOrg1[0] as Manager)!.Manage()}");
Console.WriteLine($"{(managerOrg1[0] as Worker)?.Work()}");
```

The first `WriteLine()` method will print out:

```text
I just manage and I get paid 1000000 dollars.
```

On the other hand, the second `WriteLine()` method will print nothing but a newline (because the argument evaluates to an empty string).

Since the `as` expression can result in `null`, we will need to do a null check. In this particular case, since we know that the runtime type of `managerOrg1[0]` is `Manager` (and that the expression cannot result in `null`), we do a little cheating and use the `!` operator.

It is an explicit notice to the compiler that since we know what we are doing you can ignore this expression from your null checks. (`!` is called the "null forgiving operator", or the "null suppression operator".)

On the other hand, in the case of the second statement, we use the "null conditional operator", `?`. The `Work()` method will be only called if the `as` expression (before the `?`) is non-null. If the `as` expression evaluates to `null` (because `managerOrg1[0]` cannot be cast to `Worker`), then the overall value of the entire expression, `(managerOrg1[0] as Worker)?.Work()`, is null.

One thing to note is that the Management and RankAndFile classes use the "collection initialization syntax". For example,

```csharp
var managerOrg1 = new Management("M1") {
    new Manager("M1a"),
    new Manager("M1b"),
};
```

This is possible because its base class, Organization, inherits from a collection type, `List<Employee>`. Hence, these classes are effectively collection types (through inheritance).

The main program also uses a "higher order" method, `ForEach()`, which is defined as a member method on `List<T>`.

For instance,

```csharp
allEmployees.ForEach(e => total1 += e.Salary);
```

The type of the argument of `ForEach()` is a delegate. More specifically, `e => total1 += e.Salary` is a "Lambda expression", which is a sort of a literal of a delegate type.

> In this particular case, the argument of `ForEach()` is of type `Action<Employee>`. The type `Action<T>`, from the system namespace, encapsulates a method that has a single parameter and does not return a value.

A Lambda expression is like an anonymous function. Note the syntax. The variable before the fat arrow (`=>`) is an argument. If there is more than one argument, we put them in a pair of parentheses. If there is only one argument, the parentheses are typically omitted.

The expression after the fat arrow is the body of the function, an expression `total += e.Salary` in this case.

The `ForEach()` method evaluates the lambda expression for all elements of the list, `allEmployees`, in this case.

This statement is in fact equivalent to the following:

```csharp
foreach (var e in allEmployees) {
    total += e.Salary;
}
```

Although `ForEach()` is not a LINQ method, technically, it follows the same pattern as many of the LINQ methods. We will show example usages of some LINQ extension methods later in the book.

**Pop quiz.** 😃

> The constructor methods cannot be `virtual`. Why do you think that is? Likewise, constructors cannot be `abstract`. Would it make sense to have an `abstract` constructor for a type?

## Summary

We learned the basics of inheritance in C#. Virtual and `abstract` methods and properties of a type can be overridden from its subtypes, records and classes.

In particular, we used the keywords `abstract`, `virtual`, and `override`, among other things. Objects of a reference type (e.g., class, struct, and interface) can exhibit polymorphic behavior at runtime.

We also covered the six access modifiers used to control the access levels of the member methods and properties of a type. Namely, `public`, `internal`, `protected`, `protected internal`, `private protected`, and `private`.

C# provides a number of operators for checking types and casting objects between different types. We explored the some basics of the `is` and `as` operators. Although we did not cover in this lesson, C# also has an operator, `typeof`, to get the `System.Type` instance for a given type name. The `object.GetType()` method, available in all objects, can also be used to get the type of an object.

We also learned basic usages of the functional style methods (e.g., `List<T>.ForEach()`) and the lambda expressions. The `List<T>.ForEach()` method, as well as many of the LINQ extension methods, takes a delegate as one of its arguments.

# Lesson 23. Areas and Perimeters

## 23.1. Introduction

We will explore, in this lesson, how the interface multiple inheritance works in C#.

This lesson is going to be the most boring one in this book. 😞 You can skip this lesson if you are not interested in all the nitty gritty details of the C# grammar. C# is a rather complex language and in order to become proficient, however, you will at least need to be aware of certain concepts although you may not have to remember the details.

![](img/25af69ec45b3c0b589a8dccd0c2a88be_373_0.png)

## 23.2. Code Review - Area and Perimeter Calculator for Multiple Shapes

Let's start with simpler examples. How does the interface (single) inheritance works in C#.

"Interface inheritance" is not the most commonly used term in this context. We more commonly say that a class "implements" an interface(s), etc. But, as long as we know what we are talking about here, what kind of terms we use is not that critical.

The complexity comes from the fact that C# gives us too many options. The choices are blessings and curses at the same time.

When we define an interface, we can optionally provide a default implementation for a method or property. When we implement an interface method or property, a class can either explicitly or implicitly implement the method or property. And so forth.

In situations like this, we often face what is called the "combinatorial explosion".

Let's take a look at some concrete examples. Here's a simple interface:

`area-calculation/si1/Area.cs` (lines 4-10)

```csharp
public interface IArea {
    /// <summary>
    /// Returns the area.
    /// This method needs to be implemented in the concrete types.
    /// </summary>
    float Size();
}
```

We will discuss more on the "XML doc comments" later. For now, the interface `IArea` declares one method `float Size()`. This interface method is implicitly abstract, and it requires an implementation in the concrete types. This method is also implicitly public.

We create three types that implement this `IArea` interface, in the `SI1` namespace (although it is not explicitly shown in the code snippets).

The `SI1.ShapeB` class "implicitly" implements the `Size()` method:

`**area-calculation/si1/Shapes.cs**` (lines 4-9)

```csharp
public class ShapeB : IArea {
    /// <summary>Implicit/normal implementation of
    /// IArea.Size().</summary>
    public float Size() {
        return 5.0f;
    }
}
```

This is the most common, and traditional, way of implementing an interface method or property. Let's test it with a simple program:

```csharp
ShapeB shape1B = new();
var size1B = shape1B.Size();
Console.WriteLine($"size1B = {size1B}");
```

This outputs, as expected,

```text
size1B = 5
```

Not much surprise here. Now, let's try the "explicit implementation":

`**area-calculation/si1/Shapes.cs**` (lines 12-17)

```csharp
public class ShapeC : IArea {
    /// <summary>Explicit implementation of IArea.Size().</summary>
    float IArea.Size() {
        return 10.0f;
    }
}
```
