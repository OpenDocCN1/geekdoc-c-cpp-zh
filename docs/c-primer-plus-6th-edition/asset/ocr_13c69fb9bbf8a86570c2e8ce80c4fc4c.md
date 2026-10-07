# Bitwise Operators 1239

| a | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 1 |
| b | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 |
| a^b | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 1 | 0 | 1 |

1 because corresponding bit in b is 1 0 because corresponding bits in a and b are 0 1 because corresponding bit in a is 1 0 because corresponding bits in a and b are 1

Figure E.5 The bitwise XOR operator.

# Table E.2 The Value of b1 ^ b2

| Bit Values | b1 = 0 | b1 = 1 |
| b2 = 0 | 0 | 1 |
| b2 = 1 | 1 | 0 |

The ^= operator combines the bitwise XOR operator with assignment:
a ^= b; // set a to a ^ b

The bitwise AND operator (&) combines two integer values to produce a new integer value. Each bit in the new value is set to 1 only if both of the corresponding bits in the original values are set to 1. If either or both corresponding bits are 0, the final bit is set to 0 (see Figure E.6).

| a | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 1 | 0 |
| b | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 |
| a&b | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |

0 because only one corresponding bit is 1 0 because corresponding bits in a and b are 0 1 because corresponding bits in a and b both are 1

Figure E.6 The bitwise AND operator.