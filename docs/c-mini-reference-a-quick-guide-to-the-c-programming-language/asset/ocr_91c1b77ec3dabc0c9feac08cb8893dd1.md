# 5. C# Type System

C#, and .NET, has a unified type system. Every type in the C# language inherits, either directly or indirectly, from the object base type on .NET).

The types in C# are divided into two main categories, reference types and value types. Variables of the value types may directly contain their data, whereas variables of the reference types store references to their data. Values of reference types are treated as objects simply by viewing the values as type On the other hand, values of value types are treated as objects by performing boxing and unboxing operations.

Generic types are discussed later. Generic type parameters can designate either a value type or a reference type.