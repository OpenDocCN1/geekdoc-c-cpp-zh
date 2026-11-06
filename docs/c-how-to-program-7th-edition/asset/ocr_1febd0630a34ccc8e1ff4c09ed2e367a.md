```
```
31
32        if ( i % 8 == 0 ) // output a space after 8 bits
33            cout << ' ';
34        } // end for
35
36    cout << endl;
37 } // end function displayBits
```
```

```
```
Enter an unsigned integer: 65000
        65000 = 00000000 00000000 11111101 11101000
```
```

```
```
Enter an unsigned integer: 29
            29 = 00000000 00000000 00000000 00011101
```
```

Fig. 21.6 | Printing an unsigned integer in bits. (Part 2 of 2.)

Function displayBits (lines 19–37) uses the bitwise AND operator to combine variable value with constant MASK. Often, the bitwise AND operator is used with an operand called a mask—an integer value with specific bits set to 1. Masks are used to hide some bits in a value while selecting other bits. In displayBits, line 22 assigns constant MASK the value 1 << SHIFT. The value of constant SHIFT was calculated in line 21 with the expression

```
```
8 * sizeof( unsigned ) - 1
```
```

which multiplies the number of bytes an unsigned object requires in memory by 8 (the number of bits in a byte) to get the total number of bits required to store an unsigned object, then subtracts 1. The bit representation of 1 << SHIFT on a computer that represents unsigned objects in four bytes of memory is

```
```
10000000 00000000 00000000 00000000
```
```

The left-shift operator shifts the value 1 from the low-order (rightmost) bit to the high-order (leftmost) bit in MASK, and fills in 0 bits from the right. Line 29 prints a 1 or a 0 for the current leftmost bit of variable value. Assume that variable value contains 65000 (00000000 00000000 11111101 11101000). When value and MASK are combined using &, all the bits except the high-order bit in variable value are “masked off” (hidden), because any bit “ANDed” with 0 yields 0. If the leftmost bit is 1, value & MASK evaluates to

```
```
00000000 00000000 11111101 11101000    (value)
10000000 00000000 00000000 00000000    (MASK)
--------------------------------
00000000 00000000 00000000 00000000    (value & MASK)
```
```

which is interpreted as false, and 0 is printed. Then line 30 shifts variable value left by one bit with the expression value <<= 1 (i.e., value = value << 1). These steps are repeated for each bit variable value. Eventually, a bit with a value of 1 is shifted into the leftmost bit position, and the bit manipulation is as follows:

```
```
11111101 11101000 00000000 00000000    (value)
10000000 00000000 00000000 00000000    (MASK)
--------------------------------
10000000 00000000 00000000 00000000    (value & MASK)
```
```