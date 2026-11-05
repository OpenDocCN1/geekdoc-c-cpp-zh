For a given source type S and target type T, if S or T are nullable value types, let S₀ and T₀ refer to their underlying types; otherwise, S₀ and T₀ are equal to S and T respectively. A class or struct is permitted to declare a conversion from a source type S to a target type T only if all of the following are true:

+   - S₀ and T₀ are different types.
+   - Either S₀ or T₀ is the instance type of the class or struct that contains the operator declaration.
+   - Neither S₀ nor T₀ is an interface_type.
+   - Excluding user-defined conversions, a conversion does not exist from S to T or from T to S.

For the purposes of these rules, any type parameters associated with S or T are considered to be unique types that have no inheritance relationship with other types, and any constraints on those type parameters are ignored.

*Example: In the following:*

```
class <T> {...}

class D<T> : C<T>
{
    public static implicit operator C<int>(D<T> value) {...}    // Ok
    public static implicit operator C<string>(D<T> value) {...} // Ok
    public static implicit operator C<T>(D<T> value) {...}      // Error
}
```

the first two operator declarations are permitted because T and int and string, respectively are considered unique types with no relationship. However, the third operator is an error because C<T> is the base class of D<T>.

*end example*

From the second rule, it follows that a conversion operator shall convert either to or from the class or struct type in which the operator is declared.

*Example: It is possible for a class or struct type C to define a conversion from C to int and from int to C, but not from int to bool. end example*

It is not possible to directly redefine a pre-defined conversion. Thus, conversion operators are not allowed to convert from or to object because implicit and explicit conversions already exist between object and all other types. Likewise, neither the source nor the target types of a conversion can be a base type of the other, since a conversion would then already exist. However, it is possible to declare operators on generic types that, for particular type arguments, specify conversions that already exist as pre-defined conversions.

*Example:*

```
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```

when type object is specified as a type argument for T, the second operator declares a conversion that already exists (an implicit, and therefore also an explicit, conversion exists from any type to type object).

*end example*