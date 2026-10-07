© ISO/IEC 2011 – All rights reserved ISO/IEC 9899:2011 (E)

+   - An object or expression with an integer type (other than **int** or **unsigned int**) whose integer conversion rank is less than equal to the rank of **int** and **unsigned int**.
- A bit-field of type **Bool**, **int**, **signed int**, or **unsigned int**.

If an **int** can represent all values of the original type (as restricted by the width, for a bit-field), the value is converted to **int**; otherwise, it is converted to an **unsigned int**. These are called the *integer promotions*.⁵58 All other types are unchanged by the integer promotions.

The integer promotions preserve value including sign. As discussed earlier, whether a “plain” **char** is treated as signed or implementation-defined.

**Forward references:** enumeration specifiers (6.7.2.2), structure and union specifiers (6.7.2.1).

# 6.3.1.2 Boolean type

When any scalar value is converted to **Bool**, the result is 0 if the value compares to 0; otherwise, the result is 1⁵⁹

# 6.3.1.3 Signed and unsigned integers

When a value with integer type is converted to another integer type than **Bool**, if the value can be represented by the new type, it is unchanged.

Otherwise, if the new type is unsigned, the value is converted by repeatedly adding or subtracting one than the maximum value that can be represented in the new type until the value is in the range of the new type.⁶⁰

Otherwise, the new type is signed and the value cannot be represented in it; either the result is implementation-defined or an implementation-defined signal is raised.

# 6.3.1.4 Real floating and integer

When a value of real floating type is converted to another integer type than **Bool**, the fractional part is discarded (i.e., the value is truncated toward zero). If the value of the integral part cannot be represented by the integer type, the behavior is undefined.⁶¹

> ⁵⁸ The integer promotions are applied only; as part of the usual arithmetic conversions, certain arguments apply, to the operands of the unary +, - operators, and to both operands of the shift operators, by their respective sequences.
⁵⁹ NaNs do not compare equal to 0 and convert to 1.

> ⁶⁰ The rules describe arithmetic on the mathematical value, not the value of a given expression.
⁶¹ The remaining operation performed when a value of real floating type is converted to unsigned type. Thus, the range of portable floating values is (-1, _Utype_MAX+1).

# 6.3.1.4

Language 51