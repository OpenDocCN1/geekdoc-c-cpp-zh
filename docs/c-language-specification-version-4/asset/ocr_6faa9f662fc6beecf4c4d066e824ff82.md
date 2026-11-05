The formal parameter list consists of one or more comma-separated parameters of which only the last may be a parameter-array.

A fixed-parameter consists of an optional set of attributes (§17), an optional ref, out or this modifier, a type, an identifier and an optional default-argument. Each fixed-parameter declares a parameter of the given type with the given name. The this modifier designates the method as an extension method and is only allowed on the first parameter of a static method. Extension methods are further described in §10.6.9.

A fixed-parameter with a default-argument is known as an optional parameter, whereas a fixed-parameter without a default-argument is a required parameter. A required parameter may not appear after an optional parameter in a formal-parameter-list.

A ref or out parameter cannot have a default-argument. The expression in a default-argument must be one of the following:

+   - a constant-expression
+   - an expression of the form new S() where S is a value type
+   - an expression of the form default(S) where S is a value type

The expression must be implicitly convertible by an identity or nullable conversion to the type of the parameter.

If optional parameters occur in an implementing partial method declaration (§10.2.7), an explicit interface member implementation (§13.4.1) or in a single-parameter indexer declaration (§10.9) the compiler should give a warning, since these members can never be invoked in a way that permits arguments to be omitted.

A parameter-array consists of an optional set of attributes (§17), a params modifier, an array-type, and an identifier. A parameter array declares a single parameter of the given array type with the given name. The array-type of a parameter array must be a single-dimensional array type (§12.1). In a method invocation, a parameter array permits either a single argument of the given array type to be specified, or it permits zero or more arguments of the array element type to be specified. Parameter arrays are described further in §10.6.1.4.

A parameter-array may occur after an optional parameter, but cannot have a default value – the omission of arguments for a parameter-array would instead result in the creation of an empty array.

The following example illustrates different kinds of parameters:

```
public void M(
    ref int i,
    decimal d,
    bool b = false,
    bool? n = false,
    string s = "Hello",
    object o = null,
    T t = default(T),
    params int[] a
) { }
```

In the formal-parameter-list for M, i is a required ref parameter, d is a required value parameter, b, s, o and t are optional value parameters and a is a parameter array.

A method declaration creates a separate declaration space for parameters, type parameters and local variables. Names are introduced into this declaration space by the type parameter list and the formal parameter list of the method and by local variable declarations in the block of the method. It is an error for two members of a method declaration space to have the same name. It is an error for the method declaration space and the local variable declaration space of a nested declaration space to contain elements with the same name.

A method invocation (§7.6.5.1) creates a copy, specific to that invocation, of the formal parameters and local variables of the method, and the argument list of the invocation assigns values or variable references to the