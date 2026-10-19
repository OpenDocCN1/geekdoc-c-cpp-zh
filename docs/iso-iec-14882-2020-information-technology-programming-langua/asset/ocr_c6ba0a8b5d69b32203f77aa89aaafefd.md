# 7.3.8 Floating-point promotion [conv.fpprom]

1 A prvalue of type float can be converted to a prvalue of type double. The value is unchanged.

2 This conversion is called floating-point promotion.

# 7.3.9 Integral conversions [conv.integral]

1 A prvalue of an integer type can be converted to a prvalue of another integer type. A prvalue of an unscoped enumeration type can be converted to a prvalue of an integer type.

2 If the destination type is bool, see 7.3.15. If the source type is bool, the value false is converted to zero and the value true is converted to one.

3 Otherwise, the result is the unique value of the destination type that is congruent to the source integer modulo 2^N, where N is the width of the destination type.

4 The conversions allowed as integral promotions are excluded from the set of integral conversions.

# 7.3.10 Floating-point conversions [conv.double]

1 A prvalue of floating-point type can be converted to a prvalue of another floating-point type. If the source value can be exactly represented in the destination type, the result of the conversion is that exact representation. If the source value is between two adjacent destination values, the result of the conversion is an implementation-defined choice of either of those values. Otherwise, the behavior is undefined.

2 The conversions allowed as floating-point promotions are excluded from the set of floating-point conversions.

# 7.3.11 Floating-integral conversions [conv.fpint]

1 A prvalue of a floating-point type can be converted to a prvalue of an integer type. The conversion truncates; that is, the fractional part is discarded. The behavior is undefined if the truncated value cannot be represented in the destination type.

[Note 1: If the destination type is bool, see 7.3.15. — end note]

2 A prvalue of an integer type or of an unscoped enumeration type can be converted to a prvalue of a floating-point type. The result is exact if possible. If the value being converted is in the range of values that can be represented but the value cannot be represented exactly, it is an implementation-defined choice of either the next lower or higher representable value.

[Note 2: Loss of precision occurs if the integral value cannot be represented exactly as a value of the floating-point type. — end note]

If the value being converted is outside the range of values that can be represented, the behavior is undefined. If the source type is bool, the value false is converted to zero and the value true is converted to one.