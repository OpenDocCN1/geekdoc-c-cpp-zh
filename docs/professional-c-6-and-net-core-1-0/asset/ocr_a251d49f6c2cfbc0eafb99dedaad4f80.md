across a bigger hierarchy. Class B derives from class A, and class C derives from class B. Here, class B is also known as intermediate base class. This is supported and often used with C#.

+   - **Interface inheritance**—Interface inheritance defines inheritance with interfaces. Here, multiple inheritance is possible. Interfaces and interface inheritance is explained later in this chapter in the “Interfaces” section.

Let’s discuss some specific issues with inheritance and C#.

# Multiple Inheritance

Some languages such as C++ support what is known as *multiple inheritance*, in which a class derives from more than one other class. With implementation inheritance, multiple inheritance adds complexity and also overhead to the generated code even in cases where multiple inheritance is not used. Because of this, the designers of C# decided not to support multiple inheritance with classes because support for multiple inheritance increases complexity and adds overhead even in cases when multiple inheritance is not used.

C# does allow types to be derived from multiple interfaces. One type can *implement multiple interfaces*. This means that a C# class can be derived from one other class, and any number of interfaces. Indeed, we can be more precise: Thanks to the presence of `System.Object` as a common base type, every C# class (except for `Object`) has exactly one base class, and every C# class may additionally have any number of base interfaces.

# Structs and Classes

Chapter 3 distinguishes between structs (value types) and classes (reference types). One restriction of using structs is that they do not support inheritance, beyond the fact that every struct is automatically derived from `System.ValueType`. Although it’s true that you cannot code a type hierarchy of structs, it is possible for structs to implement interfaces. In other words, structs don’t really support implementation inheritance, but they do support interface inheritance. The following summarizes the situation for any types that you define:

+   - *Structs* are always derived from `System.ValueType`. They can also be derived from any number of interfaces.

+   - *Classes* are always derived from either `System.Object` or a class that you choose. They can also be derived from any number of interfaces.

# Implementation Inheritance

If you want to declare that a class derives from another class, use the following syntax:

```
class MyDerivedClass: MyBaseClass
```