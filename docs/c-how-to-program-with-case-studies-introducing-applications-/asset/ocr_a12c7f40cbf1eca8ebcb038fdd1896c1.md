The result of right- or left-shifting a value is undefined if the right operand is negative
or if the right operand is larger than the number of bits in the left operand. The result
of right-shifting a negative number is implementation-defined.

# ### 10.9.5 Bitwise Assignment Operators

Each binary bitwise operator has a corresponding assignment operator. The following
table summarizes these bitwise assignment operators.

| Bitwise assignment operators | |
|---|---|
| &= | Bitwise AND assignment operator. |
| \|= | Bitwise inclusive OR assignment operator. |
| ^= | Bitwise exclusive OR assignment operator. |
| <<= | Left-shift assignment operator. |
| >>= | Right-shift assignment operator. |

The following table shows in decreasing order the precedence and grouping of the
operators introduced to this point in the text.

| Operator | Grouping | Type |
|---|---|---|
| () [] . -> ++ (postfix) -- (postfix) | left-to-right | highest |
| + - ++ -- ! & * ~ sizeof (type) | right-to-left | unary |
| * / % | left-to-right | multiplicative |
| + - | left-to-right | additive |
| << >> | left-to-right | shifting |
| < <= > >= | left-to-right | relational |
| == != | left-to-right | equality |
| & | left-to-right | bitwise AND |
| ^ | left-to-right | bitwise XOR |
| \| | left-to-right | bitwise OR |
| && | left-to-right | logical AND |
| \|\| | left-to-right | logical OR |
| ?: | left-to-right | conditional |
| = += -= *= /= %= &= \|= ^= <<= >>= | right-to-left | assignment |
| , | left-to-right | comma |

# ### Self Check

+   1. **(Fill-In)** Often, the bitwise AND operator is used with an operand called a
+      ________, which is an integer value with specific bits set to 1. This is used to hide some
+      bits in a value while selecting other bits.
+   
+      Answer: mask.