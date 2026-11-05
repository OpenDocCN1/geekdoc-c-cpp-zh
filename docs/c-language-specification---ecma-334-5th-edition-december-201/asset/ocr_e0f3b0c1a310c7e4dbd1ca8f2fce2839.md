infinity. To force a value of a floating-point type to the exact precision of its type, an explicit cast can be used. end example]

# 9.3.8 The decimal type

The decimal type is a 128-bit data type suitable for financial and monetary calculations. The decimal type can represent values including those in the range at least −7.9 × 10^28 to 7.9 × 10^28, with at least 28-digit precision.

The finite set of values of type decimal are of the form (−1)^s × c × 10^e, where the sign s is 0 or 1, the coefficient c is given by 0 ≤ c < Cmax, and the scale e is such that Emin ≤ e ≤ Emax, where Cmax is at least 1 × 10^28, Emin ≤ 0, and Emax ≥ 28. The decimal type does not necessarily support signed zeros, infinities, or NaN's.

A decimal is represented as an integer scaled by a power of ten. For decimals with an absolute value less than 1.0m, the value is exact to at least the 28th decimal place. For decimals with an absolute value greater than or equal to 1.0m, the value is exact to at least 28 digits. Contrary to the float and double data types, decimal fractional numbers such as 0.1 can be represented exactly in the decimal representation. In the float and double representations, such numbers often have non-terminating binary expansions, making those representations more prone to round-off errors.

If either operand of a binary operator is of decimal type then standard numeric promotions are applied, as detailed in §12.4.7, and the operation is performed with double precision.

The result of an operation on values of type decimal is that which would result from calculating an exact result (preserving scale, as defined for each operator) and then rounding to fit the representation. Results are rounded to the nearest representable value, and, when a result is equally close to two representable values, to the value that has an even number in the least significant digit position (this is known as “banker’s rounding”). That is, results are exact to at least the 28th decimal place. Note that rounding may produce a zero value from a non-zero value.

If a decimal arithmetic operation produces a result whose magnitude is too large for the decimal format, a System.OverflowException is thrown.

The decimal type has greater precision but may have a smaller range than the floating-point types. Thus, conversions from the floating-point types to decimal might produce overflow exceptions, and conversions from decimal to the floating-point types might cause loss of precision or overflow exceptions. For these reasons, no implicit conversions exist between the floating-point types and decimal, and without explicit casts, a compile-time error occurs when floating-point and decimal operands are directly mixed in the same expression.

# 9.3.9 The bool type

The bool type represents Boolean logical quantities. The possible values of type bool are true and false.

No standard conversions exist between bool and other value types. In particular, the bool type is distinct and separate from the integral types, a bool value cannot be used in place of an integral value, and vice versa.

> [Note: In the C and C++ languages, a zero integral or floating-point value, or a null pointer can be converted to the Boolean value false, and a non-zero integral or floating-point value, or a non-null pointer can be converted to the Boolean value true. In C#, such conversions are accomplished by explicitly comparing an integral or floating-point value to zero, or by explicitly comparing an object reference to null. end note]

# 9.3.10 Enumeration types

An enumeration type is a distinct type with named constants. Every enumeration type has an underlying type, which shall be byte, sbyte, short, ushort, int, uint, long or ulong. The set of values of the