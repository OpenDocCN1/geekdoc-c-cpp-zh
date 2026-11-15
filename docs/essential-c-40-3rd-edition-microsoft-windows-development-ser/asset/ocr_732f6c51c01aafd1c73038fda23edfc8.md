Customer>, Dictionary<Guid, Order>, and Dictionary<long, Order> will require new internal type definitions, for example.

# Language Contrast: Java—Generics

Sun's implementation of generics for Java occurs within the compiler entirely, not within the Java Virtual Machine. Sun did this to ensure that no updated Java Virtual Machine would need to be distributed because generics were used.

The Java implementation uses syntax similar to the templates in C++ and the generics in C#, including type parameters and constraints. But because it does not treat value types differently from reference types, the unmodified Java Virtual Machine cannot support generics for value types. As such, generics in Java do not gain the execution efficiency of C#. Indeed, whenever the Java compiler needs to return data, it injects automatic downcasts from the specified constraint, if one is declared, or the base Object type if it is not declared. Further, the Java compiler generates a single specialized type at compile time, which it then uses to instantiate any constructed type. Finally, because the Java Virtual Machine does not support generics natively, there is no way to ascertain the type parameter for an instance of a generic type at execution time, and other uses of reflection are severely limited.

# SUMMARY

Generics transformed C# 1.0 coding style. In virtually all cases in which programmers used object within C# 1.0 code, generics became a better choice in C# 2.0 and later to the extent that using object in relation to collections, at a minimum, should act as a flag for a possible generics implementation. The increased type safety, cast avoidance, and reduction of code bloat offer significant improvements. Similarly, where code traditionally used the System.Collections namespace, System.Collections.Generic should be selected instead.