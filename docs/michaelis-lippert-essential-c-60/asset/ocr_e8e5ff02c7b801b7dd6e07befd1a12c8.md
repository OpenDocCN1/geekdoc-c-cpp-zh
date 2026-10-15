# Special Floating-Point Characteristics

The binary floating-point types: float and double, have some special characteristics, such as the way they handle precision. This section looks at some specific examples, as well as some unique floating-point type characteristics.

A float, with seven decimal digits of precision, can hold the value 1,234,567 and the value 0.1234567. However, if you add these two floats together, the result will be rounded to 1234567, because the exact result requires more precision than the seven significant digits that a float can hold. The error introduced by rounding off to seven digits can become large compared to the value computed, especially with repeated calculations. (See also the Advanced Topic, “Unexpected Inequality with Floating-Point Types,” later in this section.)

Internally, the binary floating-point types actually store a binary fraction, not a decimal fraction. Consequently, “representation error” inaccuracies can occur with a simple assignment, such as `double number = 140.6F`. The exact value of 140.6 is the fraction 703/5, but the denominator of that fraction is not a power of 2, so it cannot be represented exactly by a binary floating-point number. The value actually represented is the closest fraction with a power of 2 in the denominator that will fit into the 16 bits of a float.

Since the double can hold a more accurate value than the float can store, the C# compiler will actually evaluate this expression to `double number = 140.600006103516` because 140.600006103516 is the closest binary fraction to 140.6 as a float. This fraction is slightly larger than 140.6 when represented as a double.

> **Guidelines**
> 
> **AVOID** binary floating-point types when exact decimal arithmetic is required; use the decimal floating-point type instead.

# ADVANCED TOPIC

# Unexpected Inequality with Floating-Point Types

Because floating-point numbers can be unexpectedly rounded off to non-decimal fractions, comparing floating-point values for equality can be quite confusing. Consider Listing 3.7.