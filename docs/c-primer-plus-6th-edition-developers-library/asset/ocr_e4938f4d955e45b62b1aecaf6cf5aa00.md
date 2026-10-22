The right-shift assignment operator (>>=) shifts the bits in the left-hand variable to the right by the indicated number of places, as shown here:

```
int sweet = 16;
int ooosw;
```

```
ooosw = sweet >> 3;  // ooosw = 2, sweet still 16
sweet >>=3;          // sweet changed to 2
```

# Usage: Bitwise Shift Operators

The bitwise shift operators can provide swift, efficient (depending on the hardware) multiplication and division by powers of 2:

| number << n | Multiplies number by 2 to the nth power |
| number >> n | Divides number by 2 to the nth power if number is not negative |

These shift operations are analogous to the decimal system procedure of shifting the decimal point to multiply or divide by 10.

The shift operators can also be used to extract groups of bits from larger units. Suppose, for example, you use an unsigned long value to represent color values, with the low-order byte holding the red intensity, the next byte holding the green intensity, and the third byte holding the blue intensity. Supposed you then wanted to store the intensity of each color in its own unsigned char variable. Then you could do something like this:

```
#define BYTE_MASK 0xff
unsigned long color = 0x002a162f;
unsigned char blue, green, red;
red = color & BYTE_MASK;
green = (color >> 8) & BYTE_MASK;
blue = (color >> 16) & BYTE_MASK;
```

The code uses the right-shift operator to move the 8-bit color value to the low-order byte, and then uses the mask technique to assign the low-order byte to the desired variable.

# Programming Example

In Chapter 9, “Functions,” we used recursion to write a program to convert numbers to a binary representation. Now we’ll solve the same problem by using the bitwise operators. The program in Listing 15.1 reads an integer from the keyboard and passes it and a string address to a function called itobs() (for integer-to-binary string, of course). This function then uses the bitwise operators to figure out the correct pattern of 1s and 0s to put into the string.