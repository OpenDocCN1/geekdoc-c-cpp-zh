# Chapter 4: Operators and Control Flow

# Bitwise Operators (&, |, ^)

In some instances, you might need to perform logical operations, such as AND, OR, and XOR, on a bit-by-bit basis for two operands. You do this via the &, |, and ^ operators, respectively.

# BEGINNER TOPIC

# Logical Operators Explained

If you have two numbers, as shown in Figure 4.4, the bitwise operations will compare the values of the locations beginning at the leftmost significant value and continuing until the end. The value of “1” in a location is treated as “true,” and the value of “0” in a location is treated as “false.”

| 12: | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 |

| 7: | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |

FIGURE 4.4: The 12 and 7 represented in binary

The bitwise AND of the two values in Figure 4.4 would entail the bit-by-bit comparison of bits in the first operand (12) with the bits in the second operand (7), resulting in the binary value 00000100, which is 4. Alternatively, a bitwise OR of the two values would produce 00001111, the binary equivalent of 15. The XOR result would be 00001011, or decimal 11.

Listing 4.41 demonstrates the use of these bitwise operators. The results of Listing 4.41 appear in Output 4.18.

# Listing 4.41: Using Bitwise Operators

```
byte and, or, xor;
and = 12 & 7;      // and = 4
or = 12 | 7;      // or = 15
xor = 12 ^ 7;      // xor = 11
```