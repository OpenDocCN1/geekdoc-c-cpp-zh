
The true and false unary operators require pair-wise declaration. A compile-time error occurs if a class declares one of these operators without also declaring the other. The true and false operators are described further in §12.21.

[Example: The following example shows an implementation and subsequent usage of operator++ for an integer vector class:

```csharp
public class IntVector
{
    public IntVector(int length) {...}
    public int Length { ... }  // read-only property
    public int this[int index] { ... }  // read-write indexer
    public static IntVector operator++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}
class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);   // vector of 4 x 0
        IntVector iv2;
        iv2 = iv1++;   // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;   // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

Note how the operator method returns the value produced by adding 1 to the operand, just like the postfix increment and decrement operators (§12.7.10), and the prefix increment and decrement operators (§12.8.6). Unlike in C++, this method should not modify the value of its operand directly as this would violate the standard semantics of the postfix increment operator (§12.8.6). end example]

## 15.10.3 Binary operators

The following rules apply to binary operator declarations, where T denotes the instance type of the class or struct that contains the operator declaration:

- A binary non-shift operator shall take two parameters, at least one of which shall have type T or T?, and can return any type.
- A binary << or >> operator (§12.10) shall take two parameters, the first of which shall have type T or T? and the second of which shall have type int or int?, and can return any type.

The signature of a binary operator consists of the operator token (+, -, *, /, %, &, |, ^, <<, >>, ==, !=, >, <, >=, or <=) and the types of the two formal parameters. The return type and the names of the formal parameters are not part of a binary operator's signature.

Certain binary operators require pair-wise declaration. For every declaration of either operator of a pair, there shall be a matching declaration of the other operator of the pair. Two operator declarations match if identity conversions exist between their return types and their corresponding parameter types. The following operators require pair-wise declaration:

- operator == and operator !=
- operator > and operator <
- operator >= and operator <=

## 15.10.4 Conversion operators

A conversion operator declaration introduces a user-defined conversion (§11.5), which augments the pre-defined implicit and explicit conversions.

A conversion operator declaration that includes the implicit keyword introduces a user-defined implicit conversion. Implicit conversions can occur in a variety of situations, including function member invocations, cast expressions, and assignments. This is described further in §11.2.

A conversion operator declaration that includes the explicit keyword introduces a user-defined explicit conversion. Explicit conversions can occur in cast expressions, and are described further in §11.3.

A conversion operator converts from a source type, indicated by the parameter type of the conversion operator, to a target type, indicated by the return type of the conversion operator.

For a given source type S and target type T, if S or T are nullable value types, let S0 and T0 refer to their underlying types; otherwise, S0 and T0 are equal to S and T respectively. A class or struct is permitted to declare a conversion from a source type S to a target type T only if all of the following are true:

- S0 and T0 are different types.
- Either S0 or T0 is the instance type of the class or struct that contains the operator declaration.
- Neither S0 nor T0 is an interface-type.
- Excluding user-defined conversions, a conversion does not exist from S to T or from T to S.

For the purposes of these rules, any type parameters associated with S or T are considered to be unique types that have no inheritance relationship with other types, and any constraints on those type parameters are ignored.

[Example: In the following:

```
class C<T> {...}
class D<T>: C<T>
{
    public static implicit operator C<int>(D<T> value) {...}    // Ok
    public static implicit operator C<string>(D<T> value) {...}    // Ok
    public static implicit operator C<T>(D<T> value) {...}    // Error
}
```

the first two operator declarations are permitted because T and int and string, respectively are considered unique types with no relationship. However, the third operator is an error because C<T> is the base class of D<T>. end example]

From the second rule, it follows that a conversion operator shall convert either to or from the class or struct type in which the operator is declared. [Example: It is possible for a class or struct type C to define a conversion from C to int and from int to C, but not from int to bool. end example]

It is not possible to directly redefine a pre-defined conversion. Thus, conversion operators are not allowed to convert from or to object because implicit and explicit conversions already exist between object and all other types. Likewise, neither the source nor the target types of a conversion can be a base type of the other, since a conversion would then already exist. However, it is possible to declare operators on generic types that, for particular type arguments, specify conversions that already exist as pre-defined conversions.

[Example:

```
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

when type object is specified as a type argument for T, the second operator declares a conversion that already exists (an implicit, and therefore also an explicit, conversion exists from any type to type object). end example]

In cases where a pre-defined conversion exists between two types, any user-defined conversions between those types are ignored. Specifically:

- If a pre-defined implicit conversion (§11.2) exists from type S to type T, all user-defined conversions (implicit or explicit) from S to T are ignored.
- If a pre-defined explicit conversion (§11.3) exists from type S to type T, any user-defined explicit conversions from S to T are ignored. Furthermore:
  - If either S or T is an interface type, user-defined implicit conversions from S to T are ignored.
  - Otherwise, user-defined implicit conversions from S to T are still considered.

For all types but object, the operators declared by the Convertible<T> type above do not conflict with pre-defined conversions. [Example:

```
void F(int i, Convertible<int> n) {
    i = n;                 // Error
    i = (int)n;            // User-defined explicit conversion
    n = i;                 // User-defined implicit conversion
    n = (Convertible<int>)i; // User-defined implicit conversion
}
```

However, for type object, pre-defined conversions hide the user-defined conversions in all cases but one:

```
void F(object o, Convertible<object> n) {
    o = n;                 // Pre-defined boxing conversion
    o = (object)n;         // Pre-defined boxing conversion
    n = o;                 // User-defined implicit conversion
    n = (Convertible<object>)o; // Pre-defined unboxing conversion
}
```

end example]

User-defined conversions are not allowed to convert from or to interface-types. In particular, this restriction ensures that no user-defined transformations occur when converting to an interface-type, and that a conversion to an interface-type succeeds only if the object being converted actually implements the specified interface-type.

The signature of a conversion operator consists of the source type and the target type. (This is the only form of member for which the return type participates in the signature.) The implicit or explicit classification of a conversion operator is not part of the operator's signature. Thus, a class or struct cannot declare both an implicit and an explicit conversion operator with the same source and target types.

> Note: In general, user-defined implicit conversions should be designed to never throw exceptions and never lose information. If a user-defined conversion can give rise to exceptions (for example, because the source argument is out of range) or loss of information (such as discarding high-order bits), then that conversion should be defined as an explicit conversion. end note

[Example: In the following code

```
using System;
public struct Digit
{
    byte value;
    public Digit(byte value) {
        if (value < 0 || value > 9) throw new ArgumentException();
        this.value = value;
    }
    public static implicit operator byte(Digit d) {
        return d.value;
    }
    public static explicit operator Digit(byte b) {
        return new Digit(b);
    }
}
```
