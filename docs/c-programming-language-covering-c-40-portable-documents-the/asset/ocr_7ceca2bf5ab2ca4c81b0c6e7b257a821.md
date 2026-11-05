+   - For a conversion from float or double to decimal, the source value is converted to decimal representation and rounded to the nearest number after the 28th decimal place if required (§4.1.7). If the source value is too small to represent as a decimal, the result becomes zero. If the source value is NaN, infinity, or too large to represent as a decimal, a System.OverflowException is thrown.
+   - For a conversion from decimal to float or double, the decimal value is rounded to the nearest double or float value. While this conversion may lose precision, it never causes an exception to be thrown.

> > **JOSEPH ALBAHARI** The round-to-zero behavior in the real-to-integral conversions is efficient but not always the most useful approach. For instance, under this scheme, (int) 3.9 evaluates to 3, rather than 4. C# provides no built-in mechanism for converting to the nearest integer; this capability is left to external libraries. In Microsoft's .NET Framework, the static Convert class provides this functionality via methods such as ToInt32.

# 6.2.2 Explicit Enumeration Conversions

The explicit enumeration conversions are:

+   - From sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, or decimal to any enum-type.
+   - From any enum-type to sbyte, byte, short, ushort, int, uint, long, ulong, char, float, double, or decimal.
+   - From any enum-type to any other enum-type.

An explicit enumeration conversion between two types is processed by treating any participating enum-type as the underlying type of that enum-type, and then performing an implicit or explicit numeric conversion between the resulting types. For example, given an enum-type E with an underlying type of int, a conversion from E to byte is processed as an explicit numeric conversion (§6.2.1) from int to byte, and a conversion from byte to E is processed as an implicit numeric conversion (§6.1.2) from byte to int.

# 6.2.3 Explicit Nullable Conversions

Explicit nullable conversions permit predefined explicit conversions that operate on non-nullable value types to also be used with nullable forms of those types. For each of the predefined explicit conversions that convert from a non-nullable value type S to a non-nullable value type T (§6.1.1, §6.1.2, §6.1.3, §6.2.1, and §6.2.2), the following nullable conversions exist: