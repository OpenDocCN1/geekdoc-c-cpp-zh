> **C++ NOTE:** The `newInstance` method corresponds to the idiom of a *virtual constructor* in C++. However, virtual constructors in C++ are not a language feature but just an idiom that needs to be supported by a specialized library. The `Class` class is similar to the `type_info` class in C++, and the `getClass` method is equivalent to the `typeid` operator. The Java class is quite a bit more versatile than `type_info`, though. The C++ `type_info` can only reveal a string with the name of the type, not create new objects of that type.

**java.lang.Class** 1.0

- `static Class forName(String className)`
  - returns the Class object representing the class with name `className`.
- `Constructor getConstructor(Class... parameterTypes)` 1.1
  - yields an object describing the constructor with the given parameter types. See Section 5.7.7, “Invoking Arbitrary Methods and Constructors,” on p. 286 for more information on how to supply parameter types.

**java.lang.reflect.Constructor** 1.1

- `Object newInstance(Object... params)`
  - constructs a new instance of the constructor’s declaring class, passing `params` to the constructor. See Section 5.7.7, “Invoking Arbitrary Methods and Constructors,” on p. 286 for more information on how to supply parameter types.

**java.lang.Throwable** 1.0

- `void printStackTrace()`
  - prints the Throwable object and the stack trace to the standard error stream.

# 5.7.2 A Primer on Declaring Exceptions

We cover exception handling fully in Chapter 7, but in the meantime you will occasionally encounter methods that threaten to throw exceptions.

When an error occurs at runtime, a program can “throw an exception.” Throwing an exception is more flexible than terminating the program because you can provide a *handler* that “catches” the exception and deals with it.