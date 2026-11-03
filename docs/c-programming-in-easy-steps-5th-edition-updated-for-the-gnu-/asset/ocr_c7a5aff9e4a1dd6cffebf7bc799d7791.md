# Flagging bits

By far the most common use of bitwise operators is to manipulate a compact “bit field” containing a set of Boolean “flags”. This is a much more efficient use of memory than storing Boolean flag values in separate variables – a char data type of just 1 byte can hold a bit field of eight flags, one per bit, whereas eight separate char variables would require 8 whole bytes of memory.

![](bbox=[0.1, 0.42, 0.22, 0.6])

The initial bit flags can be set by assigning a decimal value to the variable whose binary equivalent has a 1 for each bit that is to be turned “on” as a Boolean flag. For example, decimal 8 has a binary equivalent of 1000 (1x8 0x4 0x2 0x1) so turns on the fourth flag, reading from right to left from the least significant bit.

Subsequently, the bit flag values can be reversed using the bitwise NOT ~ operator but care must be taken to mask zeros before the bit flags, otherwise they will each be returned as 1. For example, to reverse a bit field of four flags within the four right bits of a byte, the four left bits must be masked. Decimal 15 is binary 0001111 (0x128 0x64 0x32 0x16 1x8 1x4 1x2 1x1) and can be applied as this mask with the bitwise AND & operator.

The bit flag pattern can also be manipulated by shifting those flags that are turned on by a specified number of bits, using the bitwise Shift left << and Shift right >> operators.

+   1. Begin a new program with a preprocessor instruction to include the standard input/output library functions
+   `#include <stdio.h>`

```
#include <stdio.h>
```