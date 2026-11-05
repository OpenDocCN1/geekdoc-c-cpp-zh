> **JON SKEET** As noted in §6.1.2, some implicit conversions from integral types to `float` or `double` can lose information. That possibility shouldn't be used as an excuse for your own user-defined implicit conversions losing information, though.

A conversion operator declaration that includes the `explicit` keyword introduces a user-defined explicit conversion. Explicit conversions can occur in cast expressions, and are described further in §6.2.

> **BILL WAGNER** In contrast to implicit conversions, explicit conversions can fail, or can lose information, because the user must explicitly ask for the conversion.

A conversion operator converts from a source type, indicated by the parameter type of the conversion operator, to a target type, indicated by the return type of the conversion operator.

For a given source type S and target type T, if S or T are nullable types, let S₀ and T₀ refer to their underlying types; otherwise, S₀ and T₀ are equal to S and T, respectively. A class or struct is permitted to declare a conversion from a source type S to a target type T only if all of the following are true:

+   - S₀ and T₀ are different types.
+   - Either S₀ or T₀ is the class or struct type in which the operator declaration takes place.
+   - Neither S₀ nor T₀ is an *interface-type*.
+   - Excluding user-defined conversions, a conversion does not exist from S to T or from T to S.

For the purposes of these rules, any type parameters associated with S or T are considered to be unique types that have no inheritance relationship with other types, and any constraints on those type parameters are ignored.

In the example

```
class C<T> { ... }
class D<T> : C<T>
{
    public static implicit operator C<int>(D<T> value) {...}  // Okay
    public static implicit operator C<string>(D<T> value) {...} // Okay
    public static implicit operator C<T>(D<T> value) {...}  // Error
}
```