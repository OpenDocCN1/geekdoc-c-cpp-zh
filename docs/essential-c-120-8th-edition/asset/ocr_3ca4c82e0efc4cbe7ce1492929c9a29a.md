# Bitwise Operators (<<, >>, |, &, ^) ~ 183

left by the number of locations specified by the operand on the right of the shift operator. Zeroes then backfill the locations on the right side of the binary number. A right-shift operator does almost the same thing in the opposite direction. However, if the number is a negative value of a signed type, the values used to backfill the left side of the binary number are 1s, rather than 0s. The shift operators are >> and <<, known as the right-shift and left-shift operators, respectively. In addition, C# includes combination shift and assignment operators, <= and =

Consider the following example. Suppose you had the int value -7, which would have a binary representation of 1111 1111 1111 1111 1111 1111 1001. In Listing 4.40 (with Output 4), right-shift the binary representation of the number -7 by two locations.

# Listing 4.40: Using the Right-Shift Operator

```
int x;
x = (-7 >> 2); // 11111111111111111111111111111001 becomes
                // 11111111111111111111111111111110
// Write out "x is -2".
Console.WriteLine($"x = {x}");
```

# OUTPUT 4.17

| x = -2 |

Because of the right shift, the value of the bit in the rightmost location has "dropped off" the edge, and the negative bit indicator on the left shifts by two locations to be replaced with 1s. The result is -2.

Although legend has that x << 2 is faster than x * 4, you should not use bit-shift operators for multiplication or division. This difference might held true for certain C compilers in the 1970s, but modern compilers and modern microprocessors are perfectly capable of optimizing arithmetic. Using shifting for multiplication or division is confusing and frequently leads to errors when code maintainers forget that the shift operators have lower precedence than the arithmetic operators.