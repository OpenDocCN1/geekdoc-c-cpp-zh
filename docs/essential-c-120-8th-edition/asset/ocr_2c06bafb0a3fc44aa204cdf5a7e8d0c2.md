# Chapter 9: Introducing Structs and Records

Minutes, and Seconds are equal (and potentially any other properties that the Angle includes). Therefore, it is almost always necessary to provide a custom implementation of value equality on a value type.

Value equality is not limited to value types, however. Value type equality might also make sense on a reference type. string is a great example. Although string is a reference type, the comparison of two strings should be equal if all the letters in the string are identical, even if the two strings are different instances.

In addition, a correct override of Equals() requires a host of additional members to exist and potentially be overridden, described later in the section “Implementing Value Equality” (https://essentialsharp.com/implementing-value-equality). These include GetHashCode() and the == and != operators. Before then, let's delve into what a value type is.

> NOTE The implementation of object.Equals(), the default implementation on all objects before overriding, relies on ReferenceEquals() alone. All value value types override the default implementation to instead compare one or more values within the value type. Reference types can optionally also override Equals() to support value equality. It is always necessary to implement equality on custom value types.

# Structs

The C# built-in types, such as bool and int, are value types, except for string and object, which are reference types. Numerous additional value types are provided within the framework. Developers can also define their own value types.

To define a custom value type, you use a syntax similar to the syntax you would use to define class and interface types. The key difference in the syntax is that value types use the keyword struct (Listing 9.1).

Unfortunately, the commented-out ellipses represent a host of complexity as we will come to see later in the chapter.