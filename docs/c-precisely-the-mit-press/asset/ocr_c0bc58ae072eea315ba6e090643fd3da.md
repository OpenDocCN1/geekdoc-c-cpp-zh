# 26 Generic Types and Methods

Generic methods provide a way to strengthen type check at compile-time, to avoid type checks and casts at run-time, and to improve run-time data representation, while at the same time making programs more expressive, reusable, and readable. The ability to have generic types and methods is also known as parametric polymorphism.

# 26.1 Generics: Safety, Generality, and Efficiency

The original C# (and Java) language did not support generic types and methods. Therefore a library for manipulating arbitrary kinds of values would have to cast those values to type object. For instance, ArrayList could be used to hold Person objects, but the Add method and indexer of the cool array would have to accept and return values of type object. This works but has negative consequences that can be avoided by using generic types (197 and 198).

# 26.2 Generic Types, Type Parameters, and Constructors

A generic class declaration class<T1,...,Tn> { } has one or more type parameters T1,...,Tn. The body of the declaration is an ordinary body class (section 10.1) in which the type parameters T1 can be used as if they were ordinary types (section 26.6). A generic class is also called a parametrized class.

A generic C<T1> is not itself a class. Rather, it is a mechanism or template from which classes such as C<int> or C<String> and so on, can be generated, by replacing the type parameter T1 by a type expression t1, such as int or String. The resulting classes are called constructed types. The type t1 used to replace the type parameter T1 can be any type expression: a class, an array, a struct type, an interface, a delegate type, a type dynamic, or it itself be a constructed type. However, it cannot be the pseudo-type void (which can be used only to indicate that a method has no return value), nor can it be the keyword var (section 6.3).

Generic interfaces (section 26.5), generic delegate types (section 26.8), and generic struct types (section 26.10) can be declared also, and constructed types can be created from them. Again, a generic interface is not an interface, and a generic type is not a struct, but interfaces and struct types can be constructed from generic interfaces and generic struct types.

Generic methods (section 26.7) can be declared by specifying type parameters on the method declaration in addition to any type parameters specified by the enclosing class or struct type.

The declaration of a property, indexer, operator, event, or constructor may use the type parameters of the enclosing class or struct type (example 200), but cannot have additional type parameters of its own.

Section 26.11 compares the implementation of C# generic types and methods with C++ templates and Java 5 generic types and methods.

The type parameters of generic interfaces and generic delegate types can have co- contravariant modifiers out and in (section 26.12).