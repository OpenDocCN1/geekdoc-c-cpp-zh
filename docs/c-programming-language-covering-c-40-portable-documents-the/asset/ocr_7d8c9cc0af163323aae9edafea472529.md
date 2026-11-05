A parameter-array consists of an optional set of attributes (§17), a params modifier, an array-type, and an identifier. A parameter array declares a single parameter of the given array type with the given name. The array-type of a parameter array must be a single-dimensional array type (§12.1). In a method invocation, a parameter array permits either a single argument of the given array type or zero or more arguments of the array element type to be specified. Parameter arrays are described further in §10.6.1.4.

A parameter-array may occur after an optional parameter, but cannot have a default value—the omission of arguments for a parameter-array would instead result in the creation of an empty array.

The following example illustrates different kinds of parameters:

```
```csharp
public void M(
    ref int      i,
    decimal      d,
    bool         b = false,
    bool?        n = false,
    string       s = "Hello",
    object       o = null,
    T            t = default(T),
    params int[] a
) { }
```
```

In the formal-parameter-list for M, i is a required ref parameter; d is a required value parameter; b, s, o, and t are optional value parameters; and a is a parameter array.

A method declaration creates a separate declaration space for parameters, type parameters, and local variables. Names are introduced into this declaration space by the type parameter list and the formal parameter list of the method and by local variable declarations in the block of the method. It is an error for two members of a method declaration space to have the same name. It is an error for the method declaration space and the local variable declaration space of a nested declaration space to contain elements with the same name.

A method invocation (§7.6.5.1) creates a copy, specific to that invocation, of the formal parameters and local variables of the method, and the argument list of the invocation assigns values or variable references to the newly created formal parameters. Within the block of a method, formal parameters can be referenced by their identifiers in simple-name expressions (§7.6.2).

There are four kinds of formal parameters:

+   - Value parameters, which are declared without any modifiers.
+   - Reference parameters, which are declared with the ref modifier.
+   - Output parameters, which are declared with the out modifier.
+   - Parameter arrays, which are declared with the params modifier.