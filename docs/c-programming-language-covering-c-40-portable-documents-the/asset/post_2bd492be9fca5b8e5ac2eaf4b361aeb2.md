
> **VLADIMIR RESHETNIKOV** The Microsoft C# compiler does not check whether SE and TE are reference types; it only checks whether the explicit conversion from SE to TE is classified as an explicit reference conversion. See the corresponding annotation in §6.1.6 for details.

- From System.Array and the interfaces it implements to any array type.
- From a single-dimensional array type S[] to System.Collections.Generic.IList<T> and its base interfaces, provided that there is an explicit reference conversion from S to T.
- From System.Collections.Generic.IList<S> and its base interfaces to a single-dimensional array type T[], provided that there is an explicit identity or reference conversion from S to T.
- From System.Delegate and the interfaces it implements to any delegate type.
- From a reference type to a reference type T, if it has an explicit reference conversion to a reference type T₀ and T₀ has an identity conversion to T.
- From a reference type to an interface or delegate type T, if it has an explicit reference conversion to an interface or delegate type T₀ and either T₀ is variance-convertible to T or T is variance-convertible to T₀ (§13.1.3.2).
- From D<S₁...Sₙ> to D<T₁...Tₙ>, where D<X₁...Xₙ> is a generic delegate type, D<S₁...Sₙ> is not compatible with or identical to D<T₁...Tₙ>, and for each type parameter Xᵢ of D the following holds:
  - If Xᵢ is invariant, then Sᵢ is identical to Tᵢ.
  - If Xᵢ is covariant, then there is an implicit or explicit identity or reference conversion from Sᵢ to Tᵢ.
  - If Xᵢ is contravariant, then Sᵢ and Tᵢ are either identical or both reference types.

> **ERIC LIPPERT** The justification of this last point is that you might have a variable of type Action<S>, where S is a reference type that contains an instance of Action<object>. You can implicitly convert an Action<object> to Action<T>, where T is any reference type, so you should be able to explicitly convert Action<S> to Action<T> for any reference types S and T.

- Explicit conversions involving type parameters that are known to be reference types. For more details on explicit conversions involving type parameters, see §6.2.6.

The explicit reference conversions are those conversions between reference types that require runtime checks to ensure they are correct.

For an explicit reference conversion to succeed at runtime, the value of the source operand must be null, or the actual type of the object referenced by the source operand must be a type that can be converted to the destination type by an implicit reference conversion (§6.1.6) or boxing conversion (§6.1.7). If an explicit reference conversion fails, a System.InvalidCastException is thrown.

Reference conversions, implicit or explicit, never change the referential identity of the object being converted. In other words, while a reference conversion may change the type of the reference, it never changes the type or value of the object being referred to.

## 6.2.5 Unboxing Conversions

An unboxing conversion permits a reference type to be explicitly converted to a value type.

An unboxing conversion exists from the types object, dynamic, and System.ValueType to any non-nullable value type, and from any interface type to any non-nullable value type that implements the interface type. Furthermore, type System.Enum can be unboxed to any enum type.

An unboxing conversion exists from a reference type to a nullable type if an unboxing conversion exists from the reference type to the underlying non-nullable value type of the nullable type.

A value type S has an unboxing conversion from an interface type I if it has an unboxing conversion from an interface type Iₐ and Iₐ has an identity conversion to I.

A value type S has an unboxing conversion from an interface type I if it has an unboxing conversion from an interface type Iₐ and either Iₐ is variance-convertible to I or I is variance-convertible to Iₐ (§13.1.3.2).

An unboxing operation consists of first checking that the object instance is a boxed value of the given value type, and then copying the value out of the instance. Unboxing a null reference to a nullable type produces the null value of the nullable type. A struct can be unboxed from the type System.ValueType, since that is a base class for all structs (§11.3.2).

Unboxing conversions are described further in §4.3.2.

## 6.2.6 Explicit Dynamic Conversions

An explicit dynamic conversion exists from an expression of type dynamic to any type T. The conversion is dynamically bound (§7.2.2), which means that an explicit conversion will be sought at runtime from the runtime type of the expression to T. If no conversion is found, a runtime exception is thrown.

If dynamic binding of the conversion is not desired, the expression can be first converted to object, and then to the desired type.

Assume the following class is defined:

```csharp
class C
{
    int i;
    public C(int i) { this.i = i; }
    public static explicit operator C(string s)
    {
        return new C(int.Parse(s));
    }
}
```

The following example illustrates explicit dynamic conversions:

```csharp
object o = "1";
dynamic d = "2";
var c1 = (C)o; // Compiles, but explicit reference conversion fails
var c2 = (C)d; // Compiles and user-defined conversion succeeds
```

The best conversion of o to C is found at compile time to be an explicit reference conversion. This fails at runtime, because "1" is not, in fact, a C. The conversion of d to C as an explicit dynamic conversion, however, is suspended to runtime, where a user-defined conversion from the runtime type of d—string—to C is found, and succeeds.

## 6.2.7 Explicit Conversions Involving Type Parameters

The following explicit conversions exist for a given type parameter T:

- From the effective base class C of T to T and from any base class of C to T. At runtime, if T is a value type, the conversion is executed as an unboxing conversion. Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.
- From any interface type to T. At runtime, if T is a value type, the conversion is executed as an unboxing conversion. Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.
- From T to any interface type I, provided there is not already an implicit conversion from T to I. At runtime, if T is a value type, the conversion is executed as a boxing conversion followed by an explicit reference conversion. Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.
- From a type parameter U to T, provided T depends on U (§10.1.5). At runtime, if U is a value type, then T and U are necessarily the same type and no conversion is performed. Otherwise, if T is a value type, the conversion is executed as an unboxing conversion. Otherwise, the conversion is executed as an explicit reference conversion or identity conversion.

If T is known to be a reference type, all of these conversions are classified as explicit reference conversions (§6.2.4). If T is not known to be a reference type, these conversions are classified as unboxing conversions (§6.2.5).

> **JOSEPH ALBAHARI** The behavior of conversions involving type parameters can be further illustrated with the following method:
>
> ```csharp
> static T Cast<T>(object value) { return (T)value; }
> ```
>
> This method can perform a reference conversion or an unboxing, but never a numeric or user-defined conversion:
>
> ```csharp
> string s = Cast<string>("s");
> // Okay - reference conversion
> int i = Cast<int>(3);
> // Okay - unboxing
> long l = Cast<long>(3);
> // InvalidCastException: attempts
> // an unboxing instead of an
> // int -> long numeric conversion
> ```
>
> An identical situation arises in the method System.Linq.Enumerable.Cast, which is a standard query operator in Microsoft's LINQ implementation.

The above rules do not permit a direct explicit conversion from an unconstrained type parameter to a non-interface type, which might be surprising. The reason for this rule is to prevent confusion and make the semantics of such conversions clear. For example, consider the following declaration:

```csharp
class X<T>
{
    public static long F(T t) {
        return (long)t; // Error
    }
}
```

If the direct explicit conversion of t to long were permitted, one might easily expect that X<int>.F(7) would return 7L. However, it would not, because the standard numeric conversions are considered only when the types are known to be numeric at binding time. To make the semantics clear, the above example must instead be written:

```csharp
class X<T>
{
    public static long F(T t) {
        return (long)(object)t; // Okay, but works only when T is long
    }
}
```

This code will now compile, but executing X<int>.F(7) would then throw an exception at runtime, because a boxed int cannot be converted directly to a long.
