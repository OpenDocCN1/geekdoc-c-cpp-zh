# Chapter 15

# 797

The Shift Operators

![](bbox=[0.327, 0.126, 0.672, 0.355])

Figure 15.3 An example of a left shift

For unsigned integers, each left shift corresponds to multiplication by two. This is also true for signed numbers using two complement representation, as long as the leftmost bit doesn't switch values. Because a change in the leftmost bit of a twos complement number represents a change in both the sign and magnitude represented by the bit, this shift doesn't represent a simple multiplication by two.

The right shift operator,>> causes the bits in an operand to be shifted to the right by three bit positions. For a given amount. For example, the statement

```
op2 = op1 >> 3;
```

causes the bits in op1 to be shifted to the right by binary number 11110000101011. Figure 15.4a illustrates the right shift of the unsigned binary bits are shifted 'off the end' and are lost. As shown, the three rightmost bits are shifted three bit positions.

![](bbox=[0.327, 0.633, 0.672, 0.862])

Figure 15.4a An unsigned arithmetic right shift