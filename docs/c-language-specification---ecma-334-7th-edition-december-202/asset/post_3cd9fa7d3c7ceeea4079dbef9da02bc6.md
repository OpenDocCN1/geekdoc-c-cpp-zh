
- From sbyte to byte, ushort, uint, ulong, or char.
- From byte to sbyte or char.
- From short to sbyte, byte, ushort, uint, ulong, or char.
- From ushort to sbyte, byte, short, or char.
- From int to sbyte, byte, short, ushort, uint, ulong, or char.
- From uint to sbyte, byte, short, ushort, int, or char.
- From long to sbyte, byte, short, ushort, int, uint, ulong, or char.
- From ulong to sbyte, byte, short, ushort, int, uint, long, or char.
- From char to sbyte, byte, or short.
- From float to sbyte, byte, short, ushort, int, uint, long, ulong, char, or decimal.
- From double to sbyte, byte, short, ushort, int, uint, long, ulong, char, float, or decimal.
- From decimal to sbyte, byte, short, ushort, int, uint, long, ulong, char, float, or double.

Because the explicit conversions include all implicit and explicit numeric conversions, it is always possible to convert from any numeric_type to any other numeric_type using a cast expression (§12.9.7).

The explicit numeric conversions possibly lose information or possibly cause exceptions to be thrown. An explicit numeric conversion is processed as follows:

- For a conversion from an integral type to another integral type, the processing depends on the overflow checking context (§12.8.19) in which the conversion takes place:
  - In a checked context, the conversion succeeds if the value of the source operand is within the range of the destination type, but throws a System.OverflowException if the value of the source operand is outside the range of the destination type.
  - In an unchecked context, the conversion always succeeds, and proceeds as follows.
    - If the source type is larger than the destination type, then the source value is truncated by discarding its "extra" most significant bits. The result is then treated as a value of the destination type.
    - If the source type is the same size as the destination type, then the source value is treated as a value of the destination type
- For a conversion from decimal to an integral type, the source value is rounded towards zero to the nearest integral value, and this integral value becomes the result of the conversion. If the resulting integral value is outside the range of the destination type, a System.OverflowException is thrown.
- For a conversion from float or double to an integral type, the processing depends on the overflow-checking context (§12.8.19) in which the conversion takes place:
  - In a checked context, the conversion proceeds as follows:
    - If the value of the operand is NaN or infinite, a System.OverflowException is thrown.
    - Otherwise, the source operand is rounded towards zero to the nearest integral value. If this integral value is within the range of the destination type then this value is the result of the conversion.
    - Otherwise, a System.OverflowException is thrown.
- In an unchecked context, the conversion always succeeds, and proceeds as follows.
  - If the value of the operand is NaN or infinite, the result of the conversion is an unspecified value of the destination type.
  - Otherwise, the source operand is rounded towards zero to the nearest integral value. If this integral value is within the range of the destination type then this value is the result of the conversion.
  - Otherwise, the result of the conversion is an unspecified value of the destination type.
- For a conversion from `double` to `float`, the `double` value is rounded to the nearest `float` value. If the `double` value is too small to represent as a `float`, the result becomes zero with the same sign as the value. If the magnitude of the `double` value is too large to represent as a `float`, the result becomes infinity with the same sign as the value. If the `double` value is NaN, the result is also NaN.
- For a conversion from `float` or `double` to `decimal`, the source value is converted to `decimal` representation and rounded to the nearest number if required (§8.3.8).
  - If the source value is too small to represent as a `decimal`, the result becomes zero, preserving the sign of the original value if `decimal` supports signed zero values.
  - If the source value's magnitude is too large to represent as a `decimal`, or that value is infinity, the result is infinity preserving the sign of the original value, if the decimal representation supports infinities; otherwise a System.OverflowException is thrown.
  - If the source value is NaN, the result is NaN if the decimal representation supports NaNs; otherwise a System.OverflowException is thrown.
- For a conversion from `decimal` to `float` or `double`, the `decimal` value is rounded to the nearest `double` or `float` value. If the source value's magnitude is too large to represent in the target type, or that value is infinity, the result is infinity preserving the sign of the original value. If the source value is NaN, the result is NaN. While this conversion may lose precision, it never causes an exception to be thrown.

*Note:* The `decimal` type is not required to support infinities or NaN values but may do so; its range may be smaller than the range of `float` and `double`, but is not guaranteed to be. For `decimal` representations without infinities or NaN values, and with a range smaller than `float`, the result of a conversion from `decimal` to either `float` or `double` will never be infinity or NaN. *end note*

## 10.3.3 Explicit enumeration conversions

The explicit enumeration conversions are:

- From `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, or `decimal` to any `enum_type`.
- From any `enum_type` to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, or `decimal`.
- From any `enum_type` to any other `enum_type`.

An explicit enumeration conversion between two types is processed by treating any participating `enum_type` as the underlying type of that `enum_type`, and then performing an implicit or explicit numeric conversion between the resulting types.

Example: Given an enum_type E with an underlying type of int, a conversion from E to byte is processed as an explicit numeric conversion (§10.3.2) from int to byte, and a conversion from byte to E is processed as an implicit numeric conversion (§10.2.3) from byte to int. end example

## 10.3.4 Explicit nullable conversions

The explicit nullable conversions are those nullable conversions (§10.6.1) derived from explicit and implicit predefined conversions.

## 10.3.5 Explicit reference conversions

The explicit reference conversions are:

- From object and dynamic to any other reference_type.
- From any class_type S to any class_type T, provided S is a base class of T.
- From any class_type S to any interface_type T, provided S is not sealed and provided S does not implement T.
- From any interface_type S to any class_type T, provided T is not sealed or provided T implements S.
- From any interface_type S to any interface_type T, provided S is not derived from T.
- From an array_type S with an element type S₁ to an array_type T with an element type T₁, provided all of the following are true:
  - S and T differ only in element type. In other words, S and T have the same number of dimensions.
  - An explicit reference conversion exists from S₁ to T₁.
- From System.Array and the interfaces it implements, to any array_type.
- From a single-dimensional array_type S[] to System.Collections.Generic.IList<T>, System.Collections.Generic.IReadOnlyList<T>, and its base interfaces, provided that there is an identity conversion or explicit reference conversion from S to T.
- From System.Collections.Generic.IList<S>, System.Collections.Generic.IReadOnlyList<S>, and their base interfaces to a single-dimensional array type T[], provided that there is an identity conversion or explicit reference conversion from S to T.
- From System.Delegate and the interfaces it implements to any delegate_type.
- From a reference type S to a reference type T if it has an explicit reference conversion from S to a reference type T₀ and T₀ and there is an identity conversion from T₀ to T.
- From a reference type S to an interface or delegate type T if there is an explicit reference conversion from S to an interface or delegate type T₀ and either T₀ is variance-convertible to T or T is variance-convertible to T₀ §18.2.3.3.
- From D<S₁...Sₙ> to D<T₁...Tₙ> where D<X₁...Xₙ> is a generic delegate type, D<S₁...Sₙ> is not compatible with or identical to D<T₁...Tₙ>, and for each type parameter Xᵢ of D the following holds:
  - If Xᵢ is invariant, then Sᵢ is identical to Tᵢ.
  - If Xᵢ is covariant, then there is an identity conversion, implicit reference conversion or explicit reference conversion from Sᵢ to Tᵢ.
  - If Xᵢ is contravariant, then Sᵢ and Tᵢ are either identical or both reference types.
