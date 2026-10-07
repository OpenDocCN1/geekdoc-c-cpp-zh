```
// ...
}
```

Although this option requires only one implementation of a nullable type, the runtime always boxes value types when setting the Value property. Furthermore, retrieving the underlying value from the Value property requires a cast operation, which might potentially be invalid at runtime.

Neither option is particularly attractive. To eliminate this problem, generics¹ were added to C#. (And, in fact, nullable types are implemented as the generic Nullable<T>.)

# Introducing Generic Types

Generics provide a facility for creating data structures that can be specialized to handle specific types. Programmers define these parameterized types so that each variable of a particular generic type has the same internal algorithm, but the types of data and method signatures can vary on the basis of the type arguments provided for the parameters.

To minimize the learning curve for developers, the C# designers chose syntax that superficially resembles C++ templates. In C#, the syntax for generic classes and structures use angle brackets to both declare the generic type parameters in the type declaration and specify the generic type arguments when the type is used.

# Using a Generic Class

Listing 12.6 shows how you can specify the actual type used by the generic class. You instruct the path variable to be the “Stack of Cell” type by specifying Cell within angle bracket notation in both the object creation expression and the declaration statement. In other words, when declaring a variable (path in this case) using a generic data type, C# requires the developer to identify the actual type arguments used by the generic type. Listing 12.6 with Output 12.2 illustrates this process with the new generic Stack class.

+   1. Introduced in C# 2.0.