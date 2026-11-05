```
```csharp
IList<object> lst4 = oa1; // Ok

IList<string> lst5 = (IList<string>)oa1; // Exception
IList<string> lst6 = (IList<string>)oa2; // Ok

IReadOnlyList<string> lst7 = sa; // Ok
IReadOnlyList<string> lst8 = oa1; // Error, cast needed
IReadOnlyList<object> lst9 = sa; // Ok
IReadOnlyList<object> lst10 = oa1; // Ok
IReadOnlyList<string> lst11 = (IReadOnlyList<string>)oa1; // Exception
IReadOnlyList<string> lst12 = (IReadOnlyList<string>)oa2; // Ok
}
```
```

The assignment lst2 = oa1 generates a compile-time error since the conversion from object[] to IList<string> is an explicit conversion, not implicit. The cast (IList<string>)oa1 will cause an exception to be thrown at run-time since oa1 references an object[] and not a string[]. However the cast (IList<string>)oa2 will not cause an exception to be thrown since oa2 references a string[].

*end example*

Whenever there is an implicit or explicit reference conversion from S[] to IList<T>, there is also an explicit reference conversion from IList<T> and its base interfaces to S[] (§10.3.5).

When an array type S[] implements IList<T>, some of the members of the implemented interface may throw exceptions. The precise behavior of the implementation of the interface is beyond the scope of this specification.

# 17.3 Array creation

Array instances are created by array_creation_expressions (§12.8.16.5) or by field or local variable declarations that include an array_initializer (§17.7). Array instances can also be created implicitly as part of evaluating an argument list involving a parameter array (§15.6.2.6).

When an array instance is created, the rank and length of each dimension are established and then remain constant for the entire lifetime of the instance. In other words, it is not possible to change the rank of an existing array instance, nor is it possible to resize its dimensions.

An array instance is always of an array type. The System.Array type is an abstract type that cannot be instantiated.

Elements of arrays created by array_creation_expressions are always initialized to their default value (§9.3).

# 17.4 Array element access

Array elements are accessed using element_access expressions (§12.8.11.2) of the form A[I1, I2, ..., Ix], where A is an expression of an array type and each I_i is an expression of type int, uint, long, ulong, or can be implicitly converted to one or more of these types. The result of an array element access is a variable, namely the array element selected by the indices.

The elements of an array can be enumerated using a foreach statement (§13.9.5).