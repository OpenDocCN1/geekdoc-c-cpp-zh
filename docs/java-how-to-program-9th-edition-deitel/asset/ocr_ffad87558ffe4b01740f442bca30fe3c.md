+   - A generic class can be derived from another generic class. For example, generic class `Stack` (in package `java.util`) is a subclass of generic class `Vector` (in package `java.util`). We discussed these classes in Chapter 20.
+   - A nongeneric class can be derived from a generic class. For example, nongeneric class `Properties` (in package `java.util`) is a subclass of generic class `Hashtable` (in package `java.util`). We also discussed these classes in Chapter 20.
+   - Finally, a generic method in a subclass can override a generic method in a superclass if both methods have the same signatures.

# 21.10 Wrap-Up

This chapter introduced generics. You learned how to declare generic methods and classes. We discussed how backward compatibility is achieved via raw types. You also learned how to use wildcards in a generic method or a generic class. In Chapter 22, you’ll learn how to implement your own custom dynamic data structures that can grow or shrink at execution time. In particular, you’ll implement these data structures using the generics capabilities you learned in this chapter. For more information on generics, please visit our Java Resource Center at www.deitel.com/Java/ and click the topic Java Generics under the heading Resource Center Contents.

# Summary

# Section 21.1 Introduction

+   - Generic methods enable you to specify, with one method declaration, a set of related methods.
+   - Generic classes and interfaces enable you to specify sets of related types.

# Section 21.2 Motivation for Generic Methods

+   - Overloaded methods are often used to perform similar operations on different types of data.
+   - When the compiler encounters a method call, it attempts to locate a method declaration with a name and parameters that are compatible with the argument types in the method call.

# Section 21.3 Generic Methods: Implementation and Compile-Time Translation

+   - If the operations performed by several overloaded methods are identical for each argument type, they can be more compactly and conveniently coded using a generic method. A single generic method declaration can be called with arguments of different data types. Based on the types of the arguments passed to a generic method, the compiler handles each method call appropriately.
+   - All generic method declarations have a type-parameter section (p. 878) delimited by angle brackets (`<` and `>`) that precedes the method’s return type (p. 878).
+   - A type-parameter section contains one or more type parameters separated by commas.
+   - A type parameter (p. 878) is an identifier that specifies a generic type name. Type parameters can be used as the return type, parameter types and local variable types in a generic method declaration, and they act as placeholders for the types of the arguments passed to the generic method, which are known as actual type arguments (p. 878). Type parameters can represent only reference types.
+   - Type-parameter names used throughout a method declaration must match those declared in the type-parameter section. A type-parameter name can be declared only once in the type-parameter section but can appear more than once in the method’s parameter list.