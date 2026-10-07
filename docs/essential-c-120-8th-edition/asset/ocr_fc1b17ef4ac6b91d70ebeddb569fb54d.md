# Language Contrast: Java—Generics

The implementation of generics in Java occurs entirely within the compiler, not within the Java Virtual Machine. Sun Microsystems, which originally developed Java (long before Oracle took it over), adopted this approach to ensure that no updated Java Virtual Machine would need to be distributed with generics

The Java implementation uses syntax like the templates in C++ and the generics in C#, using type parameters and constraints. It does not treat value types differently from reference types, however, the unmodified Java Virtual Machine cannot support generics for value types. As such, generics in Java do not offer the same gains in execution efficiency as they do in C#. Indeed, whenever the Java compiler returns data, it injects automatic downcasts from the specified constraint, if one is declared, or the base Object type, if a constraint is not declared. Further, the Java compiler generates a single specialized type at compile time, which it uses to instantiate any constructed type. Finally, because the Java Virtual Machine does not support generics natively, there is no way to ascertain the type parameter for an instance of a generic type at execution time, and other uses of reflection are severely limited.

# Summary

In C# programs, using object (particularly in the context of any collection type) should make you consider whether the problem would be better solved with generics. The increased type safety enabled by the elimination of casts, the elimination of the boxing performance penalty, and the reduction of repeated code are all significant improvements.

Chapter 15 looks more at the most pervasive generic namespaces, .Collections.Generic. As its name implies, this namespace is composed almost exclusively of generic types. It provides clear examples of how some types that originally used objects were converted to use generics. However, before we