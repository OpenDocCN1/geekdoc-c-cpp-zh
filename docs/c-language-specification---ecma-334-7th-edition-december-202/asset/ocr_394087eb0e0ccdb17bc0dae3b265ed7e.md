binary operator consists of the operator token (+, -, *, /, %, &, |, ^, <<, >>, ==, !=, >, <, >=, or <=) and the types of the two formal parameters. The return type and the names of the formal parameters are not part of a binary operator's signature.

Certain binary operators require pair-wise declaration. For every declaration of either operator of a pair, there shall be a matching declaration of the other operator of the pair. Two operator declarations match if identity conversions exist between their return types and their corresponding parameter types. The following operators require pair-wise declaration:

+   - operator == and operator !=
+   - operator > and operator <
+   - operator >= and operator <=

# 15.10.4 Conversion operators

A conversion operator declaration introduces a user-defined conversion (§10.5), which augments the pre-defined implicit and explicit conversions.

A conversion operator declaration that includes the implicit keyword introduces a user-defined implicit conversion. Implicit conversions can occur in a variety of situations, including function member invocations, cast expressions, and assignments. This is described further in §10.2.

A conversion operator declaration that includes the explicit keyword introduces a user-defined explicit conversion. Explicit conversions can occur in cast expressions, and are described further in §10.3.

A conversion operator converts from a source type, indicated by the parameter type of the conversion operator, to a target type, indicated by the return type of the conversion operator.

For a given source type S and target type T, if S or T are nullable value types, let S0 and T0 refer to their underlying types; otherwise, S0 and T0 are equal to S and T respectively. A class or struct is permitted to declare a conversion from a source type S to a target type T only if all of the following are true:

+   - S0 and T0 are different types.
+   - Either S0 or T0 is the instance type of the class or struct that contains the operator declaration.
+   - Neither S0 nor T0 is an interface_type.
+   - Excluding user-defined conversions, a conversion does not exist from S to T or from T to S.

For the purposes of these rules, any type parameters associated with S or T are considered to be unique types that have no inheritance relationship with other types, and any constraints on those type parameters are ignored.

Example: In the following:

```
class C<T> { ... }

class D<T> : C<T>
{
    public static implicit operator C<int>(D<T> value) {...}  // Ok
    public static implicit operator C<string>(D<T> value) {...}  // Ok
    public static implicit operator C<T>(D<T> value) {...}  // Error
}
```