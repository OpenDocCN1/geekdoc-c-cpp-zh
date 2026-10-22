To avoid information peeking around the edges, a bit mask should be at least as wide as the value it's masking.

# Bitwise Shift Operators

Now let's look at C's shift operators. The bitwise shift operators shift bits to the left or right. Again, we will write binary numbers explicitly to show the mechanics.

# Left Shift: <<

The left shift operator (<<) shifts the bits of the value of the left operand to the left by the number of places given by the right operand. The vacated positions are filled with 0s, and bits moved past the end of the left operand are lost. In the following example, then, each bit is moved two places to the left:

```
(10001010) << 2  // expression
(00101000)        // resulting value
```

This operation produces a new bit value, but it doesn't change its operands. For example, suppose stonk is 1. Then stonk<<2 is 4, but stonk is still 1. You can use the left-shift assignment operator (<<=) to actually change a variable's value. This operator shifts the bit in the variable to its left by the number of places given by the right-hand value. Here's an example:

```
int stonk = 1;
int onkoo;
onkoo = stonk << 2;  /* assigns 4 to onkoo */
stonk <<= 2;         /* changes stonk to 4 */
```

# Right Shift: >>

The right-shift operator (>>) shifts the bits of the value of the left operand to the right by the number of places given by the right operand. Bits moved past the right end of the left operand are lost. For unsigned types, the places vacated at the left end are replaced by 0s. For signed types, the result is machine dependent. The vacated places may be filled with 0s, or they may be filled with copies of the sign (leftmost) bit:

```
(10001010) >> 2  // expression, signed value
(00100010)        // resulting value, some systems
(10001010) >> 2  // expression, signed value
(11100010)        // resulting value, other systems
```

For an unsigned value, you have the following:

```
(10001010) >> 2  // expression, unsigned value
(00100010)        // resulting value, all system
```

Each bit is moved two places to the right, and the vacated places are filled with 0s.