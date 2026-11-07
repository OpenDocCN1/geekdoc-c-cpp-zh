# Bitwise AND Operator (&)

Line 10 assigns the value 65535

00000000 00000000 11111111 11111111

to the integer variable number1, and line 11 assigns the value 1

00000000 00000000 00000000 00000001

to the variable mask. When you combine number1 and mask using the bitwise AND operator (&) in the expression number1 & mask (line 16), the result is

00000000 00000000 00000000 00000001

All the bits except the low-order bit in number1 are “masked off” (hidden) by “AND-ing” with variable mask.

# Bitwise Inclusive OR Operator (|)

The bitwise inclusive OR operator sets specific bits to 1 in an operand. Line 19 assigns 15

00000000 00000000 00000000 00001111

to the variable number1 and line 20 assigns 241

00000000 00000000 00000000 11110001

to the variable setBits. When you combine number1 and setBits with the bitwise inclusive OR operator in the expression number1 | setBits (line 25), the result is 255

00000000 00000000 00000000 11111111

The following table summarizes the results of combining two bits with the bitwise inclusive OR operator.

| Bit 1 | Bit 2 | Bit 1 | Bit 2 |
|---|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

# Bitwise Exclusive OR Operator (^)

The bitwise exclusive OR operator (^) sets each bit in the result to 1 if exactly one of the corresponding bits in its two operands is 1. Line 28 assigns number1 the value 139

00000000 00000000 00000000 10001011

and line 29 assigns number2 the value 199

00000000 00000000 00000000 11000111

When you combine these variables with the bitwise exclusive OR operator in the expression number1 ^ number2 (line 34), the result is

00000000 00000000 00000000 01001100