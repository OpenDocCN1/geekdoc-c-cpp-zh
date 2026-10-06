constructor for every Select projection needed. Optional parameters and named arguments offer an alternative way to simplify coding LINQ Select projection by allowing variations of a type's constructor with a lesser set of parameters. Before diving into how to use these features in LINQ queries, it is necessary to understand the syntax and limitations of these new features.

# Optional Parameters

The first new feature allows default parameters to be specified in a method signature. Callers of methods defined with default values can omit arguments without having to define a specific overload matching that lesser parameter list for convenience.

To define a default value in a method signature, you simply add a constant expression as the default value when omitted, similar to member initialization and constant definitions. A simple example method that has one mandatory parameter (p1, just like normal) and an optional parameter definition (p2) takes the following form:

```
public void MyMethod( int p1, int p2 = 5 );
```

The following invocations of method MyMethod are legal (will compile) and are functionally equivalent as far as the compiler is concerned:

```
MyMethod( 1, 5 );
MyMethod( 1 ); // the declared default for p2 (5) is used
```

The rules when defining a method signature that uses optional parameters:

+   1. Required parameters cannot appear after any optional parameter.
2. The default specified must be a constant expression available at compile time or a value type constructor without parameters, or default(T) where T is a value type.
3. The constant expression must be implicitly convertible by an identity (or null conversion) to the type of the parameter.
4. Parameters with ref or out modifier cannot be optional parameters.
5. Parameter arrays (params) can occur after optional parameters, but these cannot have a default value assigned. If the value is omitted by the calling invocation, an empty parameter array is used in either case, achieving the same results.