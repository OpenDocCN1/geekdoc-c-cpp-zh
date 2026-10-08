# 20.5 Overloading Generic Methods 865

Line 11 passes three double arguments to Maximum. Again, this is allowed because double is a synonym for Double, which implements IComparable<double>. Line 13 passes Maximum three strings, which are also IComparable<string>. We intentionally placed the largest value in a different position in each method call (lines 9, 11 and 13) to show that the generic method always finds the maximum value, regardless of its position in the argument and regardless of the inferred type.

# Value Types vs. Reference Types in Generics

In this example, the compiler generates three versions of method Maximum, based on the calls in Main. Customized Maximum methods are generated for type int and double, because string is a, third version of Maximum is generated for all reference types—the runtime then the reference type argument from the method call. For more details on how the runtime handles generics for reference type and types,

https://msdn.microsoft.com/library/f4a62ah

# 20.5 Overloading Generic Methods

A generic method each overloaded method must have a unique signature (as discussed in Chapter 7). A class can provide two or more generic methods with the same name but different method parameters. For example, we could provide a second version of generic method DisplayArray (Fig. 20.3) with the additional parameters LowIndex and High specify which position of the array to output (see Exercise 20.8).

A generic method can be overloaded by nongeneric methods with the same name. When the compiler encounters a method call, it searches for the method declaration that matches the method name and the argument types specified in the call. For example, generic method DisplayArray of Fig. 20.3 could be overloaded with a version specific to strings that outputs the strings in tabular format (see Exercise 20.9)—the non-generic version of a method takes precedence over a generic version. If the compiler cannot match a method call to either a nongeneric method or a generic method, or if there's ambiguity due to multiple matches, the compiler generates an error.

# 20.6 Generic Classes

The concept of a data structure (e.g., a stack) that contains elements can be understood independently of the element type it manipulates. A generic class provides a means for describing a class in a type-independent manner. We can then instantiate type-specific versions of the generic class. This capability is opportunity for software reusability.

With a generic class, you can use a simple, concise notation to indicate the actual type(s) that should be used in place of the class's type parameter(s). At compilation, the compiler ensures your code's type safety, and the runtime replaces type parameters with types to enable your client to interact with the generic class.

One generic class, for example, could be the basis for creating many stack classes (e.g., "Stack of double", "Stack of int", "Stack of Employee"). Figure 20.5 presents a generic class declaration. This class should not be confused with the class from namespace System.Collections.Generics. A generic class declaration is similar to a nongener class declaration, except that the class name is followed