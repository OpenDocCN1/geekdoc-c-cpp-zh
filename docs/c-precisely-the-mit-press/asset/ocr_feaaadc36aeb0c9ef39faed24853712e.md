124 Type dynamic (C# 4.0)

# 18 Type dynamic (C# 4.0)

If an expression has type dynamic, then a method call, operator application, delegate call, or field access involving expression will be resolved dynamically, at run-time, rather than compile-time. This means that any such expression will be accepted by the compiler but may fail with an exception at run-time. An expression e of compile-type dynamic will have some value; if this value is non-null, it has a run-time type, obtainable as e.GetType(). The run-time type will never be the type dynamic itself (by possibly System.Object), and will be used to resolve method calls, delegate calls, and operator operations.

If the receiver or any expression e of a method call o(..., e ...) has type dynamic, then the method call will have dynamic too, regardless of the returned types of possible target methods. In this case, the resolution of method call and the resolution of operator overload is performed at run-time, not compile-time (section 12.17.8). If no suitable method exists at run-time, RuntimeException will be thrown.

Likewise, if any of an operator is except and the operators =\, +, and so on have type dynamic, then the operator application has type dynamic also, and the operator overloading resolution is performed at run-time. In expressions such as e+=1 or o+=2, where o has type dynamic, the relevant implementation of operator will be chosen. If no such operator exists, RuntimeException will be thrown.

The expression e has type bool even when e has type dynamic.

Assignments such as x=e and x += e so have the type of x when e has type dynamic. A plain assignment to x involves evaluating e and then attempting an implicit conversion from the run-time value to the type of x. If this succeeds, the result is assigned to x; otherwise RuntimeException will be thrown.

Type dynamic can be used as the delegate type of method parameters and return types, fields, and local variables (as in for, foreach, and using statements); can be used as element types in arrays (section 9) and as generic types in generics (section 26.6); and can be used in cases.

Type dynamic cannot be used as a base class for types; as a bound in a generic parameter constraint (section 26:4); or as an argument of typeof operator. There is no System corresponding to type dynamic, and therefore there could be no result from typeof(dynamic). More, a class or struct cannot implement an interface that has type argument dynamic, such as IEnumerable<dynamic>; but it may have a well base class that has type argument dynamic, such as <dynamic>.

Type dynamic is indistinguishable from type Object in the following contexts. In method matching, for ref and out parameters; as array element type; and as argument to generic types. At run-time, type object typeof(dynamic[]) is equal to type object typeof(Object[]), and type object typeof(List<dynamic>) is equal to type object typeof(List<Object>).

See also sections 6.4 and 12.17.8 and examples 16, 101, and 102.