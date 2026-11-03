# Chapter 13

# Operations on Bits

We know that inside the computer, data is represented in binary digits called bits (0 and 1). Till now we were able to access and manipulate bytes only. But some applications, such as system programming require manipulation of individual bits within a byte. In most high-level languages this facility is not available, but C has the special feature to manipulate individual bits of a byte. This feature is implemented through bitwise operators that support bitwise operations. These bitwise operators are-

| Operator | Meaning |
|---|---|
| & | bitwise AND |
| | | bitwise OR |
| ^ | bitwise exclusive OR ( XOR ) |
| ~ | One's complement |
| << | bitwise left shift |
| >> | bitwise right shift |

Here all the operators are binary, except the complement operator, which is unary. These bitwise operators work on data of integral types only i.e. char, int, short, long including both signed and unsigned types. When these operators are applied to signed types, the result may be implementation dependent, because different implementations represent the signed data in different ways.

These operators operate on each bit of the operand, so while using these operators we'll consider the binary representation (bit pattern) of the operand. While writing the bit pattern, the numbering of bits starts from 0 and they are numbered from right to left. For example if we have an integer variable s = 0x3C60, the binary pattern of this integer is 0011 1100 0110 0000. The numbering of bits is-

![](bbox=[0.25, 0.9, 0.95, 0.97])

Here the rightmost(0th) bit is the least significant bit, while the leftmost(15th) bit is the most significant bit. A bit is on if it has value 1, while it is off if it has value 0.

We'll use a function bit_pattern() in our programs, that will take an integer as input and print the 16 bit binary pattern of that integer. The definition of this function is given in program P13.13. In our