# Special Floating-Point Characteristics

The binary floating-point types, float and double, have some special characteristics, such as the way they manage precision. This section looks at some specific examples, as well as some unique floating-point type characteristics.

A float, with seven decimal digits of precision, can hold the value 1,234,567 and the value 0.1234567. However, if you add these two floats together, the result will be rounded to 1,234,567, because the exact result requires more precision than the seven significant digits that a float can hold. The error introduced by rounding off seven digits can become large, especially with repeated calculations. (See also “Advanced Topic: Unexpected Inequality with Floating-Point Types” later in this section.)

Internally, the binary floating-point types store a binary fraction, not a decimal fraction. Consequently, “representation error” inaccuracies can occur with a simple assignment, such as double number = 140.6F. The exact value of 140.6 is the fraction 703/5, but the denominator of that fraction is not a power of 2, so a binary floating-point number cannot represent it exactly. Instead, the value represented is the closest fraction with a power of 2 in the denominator that fits into the 32 bits of float.

Since the double can hold a more accurate value than the float can store, the C# compiler actually evaluates this expression to double number = 140.600006103516 because 140.600006103516 is the closest binary fraction to 140.6 as a float. This fraction is slightly larger than 140.6 as represented as a double.

# Guidelines

+   AVOID binary floating-point types when exact decimal arithmetic is required; use the decimal floating-point type instead.