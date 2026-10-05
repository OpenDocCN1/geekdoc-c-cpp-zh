
[content]
universal character name specifying a short identifier of 0001000 or more is considered 10 characters, and each extended character is considered the same number of characters as the corresponding universal character name, if any)^{19}

- 4095 external identifiers in one translation unit
- 511 identifiers with block scope declared in one block
- 4095 macro identifiers simultaneously defined in one preprocessing translation unit
- 127 parameters in one function definition
- 127 arguments in one macro definition
- 127 arguments in one macro invocation
- 4095 characters in a logical source line
- 4095 characters in a string literal (after concatenation)
- 65535 bytes in an object (in a hosted environment only)
- 15 nesting levels for #included files
- 1023 case labels for a switch statement (excluding those for any nested switch statements)
- 1023 members in a single structure or union
- 1023 enumeration constants in a single enumeration
- 63 levels of nested structure or union definitions in a single struct-declaration-list

## 5.2.4.2 Numerical limits

An implementation is required to document all the limits specified in this subclause, which are specified in the headers <limits.h> and <float.h>. Additional limits are specified in <stdint.h>.

Forward references: integer types <stdint.h> (7.20).

## 5.2.4.1 Sizes of integer types <limits.h>

The values given below shall be replaced by constant expressions suitable for use in #if preprocessing directives. Moreover, except for CHAR_BIT and MB_LEN_MAX, the following shall be replaced by expressions that have the same type as an expression that is an object of the corresponding type converted according to the integer promotions. Their implementation-defined values shall be equal or greater in magnitude (absolute value) to those shown, with the same sign.

> 19 See “future language directions” (6.11.3).

- number of bits for smallest object that is not a bit-field (byte)
CHAR_BIT 8

- minimum value for an object of type signed char
SCHAR_MIN -127 // -(2^7 - 1)

- maximum value for an object of type signed char
SCHAR_MAX +127 // 2^7 - 1

- maximum value for an object of type unsigned char
UCHAR_MAX 255 // 2^8 - 1

- minimum value for an object of type char
CHAR_MIN see below

- maximum value for an object of type char
CHAR_MAX see below

- maximum number of bytes in a multibyte character, for any supported locale
MB_LEN_MAX 1

- minimum value for an object of type short int
SHRT_MIN -32767 // -(2^15 - 1)

- maximum value for an object of type short int
SHRT_MAX +32767 // 2^15 - 1

- maximum value for an object of type unsigned short int
USHR_MAX 65535 // 2^16 - 1

- minimum value for an object of type int
INT_MIN -32767 // -(2^15 - 1)

- maximum value for an object of type int
INT_MAX +32767 // 2^15 - 1

- maximum value for an object of type unsigned int
UINT_MAX 65535 // 2^16 - 1

- minimum value for an object of type long int
LONG_MIN -2147483647 // -(2^31 - 1)

- maximum value for an object of type long int
LONG_MAX +2147483647 // 2^31 - 1

- maximum value for an object of type unsigned long int
ULONG_MAX 4294967295 // 2^32 - 1

- minimum value for an object of type long int
LLONG_MIN -922337203684775808 // -(2⁶³ - 1)

- maximum value for an object of type long int
LLONG_MAX +922337203684775807 // 2⁶³ - 1

- maximum value for an object of type unsigned long int
ULLONG_MAX 18446744073709551615 // 2⁶⁴ - 1

If the value of an object of type char is treated as a signed integer used in an expression, the value of CHAR_MIN shall be the same as SCHAR_MIN and the value of CHAR_MAX shall be the same as UCHAR_MAX. Otherwise, the value of CHAR_MIN shall be 0 and the value of CHAR_MAX shall equal 2^CHAR_BIT - 1.

Forward references: representations of types (6.2.5), conditional inclusion (6.10.1).

### Characteristics of floating types <float.h>

The characteristics of floating types are defined in terms of a model that describes a representation of floating-point numbers and provide information about implementation’s floating-point arithmetic. The following parameters are used to define the model for each floating-point type:

- s sign (±1)
- b radix or exponent representation (integer > 1)
- e exponent (integer between minimum e and maximum e)
- p precision (the number of base-b digits in the significand)
- k nonnegative integers less than b (the significand digits)

A floating-point number (x) is defined by the following model:

```
x = sbᵏ f⁻ᵏ, e ≤ e
```

In addition to normalized floating-point numbers (f > 0 if x ≠ 0), floating types may contain other kinds of floating-point numbers, such as subnormal floating-point numbers (x ≠ 0, e = e, f = 0) and unnormalized floating-point numbers (x ≠ 0, e > e, f = 0), and values that are not floating-point numbers, such as infinities and NaNs. A NaN is an encoding signifying Not-a-Number. quiet NaN propagates through every arithmetic operation without raising a floating-point exception; signaling NaN generally raises a floating-point exception when occurring as an arithmetic operand. The floating-point model is intended to clarify the description of each floating-point characteristic and does not require the floating-point arithmetic of the implementation to be identical.

4 An implementation may give zero and values that are not floating-numbers (such as infinities and NaNs) a sign or leave them unsigned. Wherever such values are unsigned, any requirement in this International Standard to retrieve the sign shall produce an unspecified sign, and any requirement to set the sign shall be ignored.

5 The minimum range of representable values for a floating type is the most negative floating-point number representable in that type through the most positive floating-point number representable in that type. In addition, if negative infinity is representable in a type, the range of that type is extended to all negative numbers; likewise, if positive infinity is representable in a type, the range of that type is extended to all positive numbers.

7 All integer values in the <float.h> header, FLT_ROUNDS, shall be constant expressions suitable for use in #if preprocessing directives; all floating values shall be constant expressions. All except DECIMAL_DIG, FLT_EVAL_METHOD, FLT_RADIX, and FLT_ROUNDS have separate names for all three floating-point types. The floating-point model representation is provided for all values FLT_EVAL_METHOD and FLT_ROUNDS.

8 The rounding mode for floating-point addition is characterized by the implementation-defined value of FLT_ROUNDS.

-1 indeterminable
0 toward zero
1 toward nearest
2 toward positive infinity
3 toward negative infinity

All other values for FLT_ROUNDS characterize implementation-defined rounding behavior.

Except for assignment and cast (which remove extra range and precision), the values yielded by operators with floating operands subject to the usual arithmetic conversions and floating constants are evaluated to a format whose range and precision may be greater than required by the type. The use of evaluation formats is characterized by the implementation-defined value FLT_EVAL_METHOD.

- indeterminate
- evaluate all operations and constants just to the range and precision of the type;
- evaluate all operations and constants of type float and double to the range and precision of the double type, evaluate long operations and constants to the range and precision of the long double type;
- evaluate all operations and constants to the range and precision of the long double type.

All negative values for FLT_EVAL_METHOD characterize implementation-defined behavior.

10 The presence or absence of subnormal numbers is characterized by the implementation-defined values of FLT_HAS_SUNORM, DBL_HAS_SUNORM, and DBLL_HAS_SUNORM:

- indeterminate
- absent (type does not support subnormal numbers)
- present (type does support subnormal numbers)

11 The values given in the following list shall be replaced by constant expressions with implementation-defined values that are greater or equal in magnitude (absolute value) to those shown, with the same sign:

- radix of exponent representation, b
FLT_RADIX
