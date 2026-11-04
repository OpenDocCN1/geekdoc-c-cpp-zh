Rich type systems have always inspired computer scientists to do better, trying to catch more and more errors at compile time in favor of runtime checks. The way generics came along in the CLR is no different. In the early .NET 1.0 era, it was widely recognized within Microsoft that an extension to the type system would be very desirable to allow parameterized types. A little later, two researchers of Microsoft Research, Don Syme and Andrew Kennedy, improved the CLR with generic types originally code named Gyro. The rest is history, and today you can harvest this great type system-level feature addition.

# Declaring Generic Types

Let’s take a closer look at how generic types are declared. We’ve already seen the syntax used, using angle brackets < and > to specify a comma-separated list of type parameters. For example, here’s another generic collection type with two type parameters:

```
class Dictionary<TKey, TValue>
```

# VISUAL BASIC SYNTAX

When talking about generic types, use the word of to separate the name of the type from its type parameters, as denoted by angle brackets in C#. Visual Basic sounds like plain English language and uses the Of keyword to make this explicit:

```
Class List(Of T)
    '...
End Class
```

To construct a type out of the generic type, the same of keyword is used, followed by the type to be substituted for the type parameter in that position—for example, List(Of Integer).

Stylistically, generic type parameters are prefixed with a capital T, followed by a description of the parameter. This pretty much mirrors the naming convention used with interfaces, where an I prefix is used. Sometimes, especially when there’s only a single type parameter, a single letter is used, although style best practices do not recommend this.

Obviously, the names of type parameters need to be unique to avoid name clashes, just as is the case for variable names within a method. Within the declared generic type, its type parameters can be used in places where a type is expected (for example, when declaring fields, for method parameters, to declare variables).

Let’s continue our investigation of generic type declaration by taking a look at the way they get represented under the hood. For illustration purposes, consider the following fairly empty List<T> implementation: