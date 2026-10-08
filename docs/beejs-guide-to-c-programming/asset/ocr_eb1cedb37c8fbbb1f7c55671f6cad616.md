# Chapter 15. Types III: Conversions

So do we convert the character '5' (which apparently has value 53) into the value 5?

With one clever trick, that's how!

The C Standard guarantees that this character will have code points that are in sequence and in this order:

+   0 1 2 3 4 5 6 7 8 9

Ponder for a second-how can we use that? Spoilers ahead...
's look at the characters and their code points in UTF-8:

+   0 1 2 3 4 5 6 7 8 9
48 49 50 51 52 53 54 55 56 57

You will see that '5' is 53, just like we were. And '0' is 48.

So we subtract '0' from any digit character to get its numeric value:

```
char c = '0';

int x = c; // x has value 54, the code point for '6'

int y = c - '0'; // y has value 6, just like we want
And can convert the other way around, too, by adding the value on.
int x = 6;
```

```
char c = x + '0'; // c has value 54

printf("%d\n", c); // prints 54
printf("%c\n", c); // prints 6 with %c
```

You might think this is a weird way to do conversion, and by today's standards, it is certainly. But back in the old days when computers were made literally out of wood, this was the method for doing this conversion. And it didn't break, so C never fixed it.

# 15.3 Numeric Conversions

# 15.3.1 Boolean

If convert a zero to bool, the result is 0. Otherwise it's 1.

# 15.3.2 Integer to Integer Conversions

If an integer type is converted to unsigned and doesn't fit in it, the unsigned result wraps around odometer-style until it fits in the unsigned.

If an integer is converted to a signed number and doesn't fit it, the result is implementation-defined! Something unexpected will happen, but you'll have to look it up

> ⁵In practice, what's probably happening on your implementation is that the high-order bits are being dropped from the result, so a 16-bit number 0x1234 being converted to an 8-bit number ends up at 0x834, or just 0x34.

> ⁶Again, in practice, what will likely happen on your system is that the bit pattern for the original will be truncated and just used to represent the signed number, two's complement. For example, my system takes an unsigned char of 192 and converts it to signed char -64. In two's complement, the bit pattern for both numbers is binary 11000000.