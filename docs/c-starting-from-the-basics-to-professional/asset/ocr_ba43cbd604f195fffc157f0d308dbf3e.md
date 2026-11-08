Here one bit records whether the font is italic—1 signifies italic, and 0 signifies normal. Another bit specifies whether the font is bold. One byte selects one of up to 256 different styles. Five bits could record the point size up to 31 (or 32, if you disallow letters of size zero). Thus, on one 16-bit word you have four separate pieces of data. The bitwise operators provide you with the means of accessing and modifying the individual bits and groups of bits from an integer very easily so they provide you with the means of assembling and disassembling the 16-bit word.

# The Bitwise Shift Operators

The bitwise shift operators shift the contents of an integer variable by a specified number of bits to the left or right. These are used in combination with the other bitwise operators to achieve the kind of operations we described in the previous section. The >> operator shifts bits to the right, and the << operator shifts bits to the left. Bits that fall off either end of the variable are lost.

All the bitwise operations work with integers of any type, but we’ll use type short, which is usually two bytes, to keep the figures simple. Suppose you define and initialize a variable, number, with this statement:

```
```cpp
unsigned short number {16387};
```
```

You can shift the contents of this variable with this statement:

```
```cpp
auto result{ static_cast<unsigned short>(number << 2) };   // Shift left two bit positions
```
```

> > **Caution**  If you want result to have the same type as number, namely unsigned short, you have to add an explicit type conversion using `static_cast<>`. The reason is that the expression `number << 2` evaluates to a value of type int, despite the fact that number starts out as the short. There are technically no bitwise or even mathematical operators for integer types smaller than int (that is: the same would happen for, say, `number + 1`). If their operands are either char or short, they are always implicitly converted to int first. Signedness is not preserved during this conversion either.

The left operand of the left shift operator, <<, is the value to be shifted, and the right operand specifies the number of bit positions by which the value is to be shifted. Figure 3-2 shows the effect.