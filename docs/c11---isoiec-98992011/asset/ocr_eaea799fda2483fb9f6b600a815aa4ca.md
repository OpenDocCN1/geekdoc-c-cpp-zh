# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – All rights reserved

the resulting value. If the sign bit is 1, the value shall be modified in one of the following ways:

+   - the corresponding value with sign bit 0 is negated (sign and magnitude);
- the sign bit has the value -(2^M) (*two’s complement*);
- the sign bit has the value -(2^M - 1) (*ones’ complement).

Which of these applies is implementation-defined, as whether the value with sign bit 1 and all value bits zero (the first two), or with sign bit and all value bits 1 (ones' complement), is a trap representation or a normal value. In the case of sign and magnitude and ones' complement, if this representation is a normal value it is called a negative zero.

+   If the implementation negative zeros, they shall be generated only by:
- the &, ^, ~, <<, and >> operators with operands that produce such a value;
- the +, -, *, /, and % operators where one operand is a negative zero and the result is zero;
- compound assignment operators based on the above cases.

It is unspecified whether these cases actually generate a negative zero or a normal value, and whether a negative zero becomes a normal zero stored in an object.

If the implementation does not support negative zeros, the behavior of the &, ^, ~, <<, and >> operators that would produce such a value is undefined.

The values of any padding bits are unspecified.⁵⁴⁾ A valid (non-trap) object representation of a signed integer type where the sign bit is zero is a valid object representation of the corresponding unsigned type, and shall represent the same value. For any integer, the object representation where all the bits are zero shall be a representation of the value zero in that type.

The precision of an integer is the number of bits to represent values, excluding any sign and padding bits. The width of an integer type is the same but including any sign bit; thus for unsigned integer types the two values are the same, while for signed types the width is greater than the precision.

> ⁵⁴) Some combinations of padding bits might generate trap representations, for example, if one padding bit is a parity bit. Regardless, no arithmetic operation on valid values can generate a trap representation other than part of an exceptional condition such as overflow. All combinations of padding bits are alternative object representations of the value specified by the value bits.

46

Language

§6.2.6.2

****