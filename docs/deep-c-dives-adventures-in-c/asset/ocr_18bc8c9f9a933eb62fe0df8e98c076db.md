The bitwise operators work with integer types. For example:

```
int a = 0xF0;  
int b = 0xFF;  
int c = ~a & b;  
printf("%X\n",c)
```

This first works out the bitwise NOT of a, i.e. 0F. This is then bitwise ANDed with b, i.e. 0F & FF which is F. The %X format specifier prints the value in hex. You can use %x for lower case and %d for decimal.

# ## Signed v Unsigned

Now we come to a subtle and troublesome point. Bitwise operators are only uniquely defined for unsigned values. The reason is that unsigned values have an unambiguous representation in binary and hence the operations are well-defined in terms of the values the bit patterns represent.

That is:

```
unsigned int value=5;
```

is always 0101 and hence:

```
value | 0x2
```

is not only always 0111, but also always represents +7.

The same is not true for signed values simply because the way in which negative numbers are represented isn’t fixed. The most common representation is two’s complement, but this is not part of the C language standard, before C23, and so logical operations on unsigned numbers are implementation-dependent. The C23 standard changes this and makes two’s- complement mandatory for negative values, but it will be some time before this comes widely into effect. Notice that this does not mean logical operations on signed values are undefined behavior – if this was the case most C programs would stop working properly. In addition “implementation- dependent” has one fairly consistent meaning:

> > take the bit pattern that represents the value and perform the specified logical operation as if everything involved was an unsigned value.

This is the only sane way to deal with the problem and it is exactly what you would expect.