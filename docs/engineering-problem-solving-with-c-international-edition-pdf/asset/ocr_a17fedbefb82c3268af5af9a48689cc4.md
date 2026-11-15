```
/*---- Pixel::validate() -----------------------*/
void Pixel::validate()
{
    if(red > MAXVAL) overflowFlag = overflowFlag|RMASK;
    if(green > MAXVAL) overflowFlag = overflowFlag|GMASK;
    if(blue > MAXVAL) overflowFlag = overflowFlag|BMASK;
}
```

![](bbox=[0.13, 0.23, 0.2, 0.3])

Notice that the private mutator method `void Pixel::validate()` uses the bitwise operator `|` to set the state of `overflowFlag`. The method `validate()` must be called by all mutator methods of the `Pixel` class to guarantee the correct state of `overflowFlag`. The public accessor method `bool Pixel::overflow()` uses the bitwise operator `&` to return the state of `overflowFlag`. We will look at these two methods in more detail and also discuss bitwise operators.

# Bitwise Operators

A bitwise operator performs an operation on each bit of its operand. C++ supports three binary bitwise operators: the bitwise or (`|`), the bitwise and (`&`) and the bitwise exclusive or (`^`), and a unary bitwise not operator(`~`). The operands for these operators are restricted to be of an integral type, such as `int` or `char`. Table 10.2 provides a truth table for bitwise operators.

| A | B | ~A | A|B | A^B | A&B |
|---|---|---|---|---|---|
| 0001 | 0001 | 1110 | 0001 | 0000 | 0001 |
| 0010 | 0010 | 1101 | 0010 | 0000 | 0010 |
| 0011 | 0100 | 1100 | 0111 | 0111 | 0000 |
| 0100 | 0111 | 1011 | 0111 | 0011 | 0100 |

To illustrate the use of bitwise operators, assume that a `Pixel` object has been defined and has the following value:

```
Pixel p1   278   unsigned red
           298   unsigned green
           150   unsigned blue
           0     unsigned short overflowFlag
```

The statement `p1.validate();` results in the following program trace and memory snapshot: