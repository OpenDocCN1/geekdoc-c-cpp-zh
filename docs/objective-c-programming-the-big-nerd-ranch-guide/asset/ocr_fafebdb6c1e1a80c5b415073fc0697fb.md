# 33  
Bitwise Operations

In the first part of this book, I described the memory of a computer as a vast meadow of switches (billions of switches) that could be turned on or off. Each switch represents one bit, and we usually use 1 to mean "on" and 0 to mean "off."

However, you never address a single bit. Instead, you deal with byte-sized chunks of bits. If you think of a byte as an unsigned 8-bit integer, each bit represents another power of two:

# Figure 33.1  One byte representing the decimal number 60

128 64 32 16 8 4 2 1
| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 |
32 + 16 + 8 + 4 = 60

As a side-effect of living with 10 fingers, people like to work with decimal numbers (base-10). Computers, however, like powers of 2. Programmers often use a base-16 number system ($16 = 2^4$) known as *hexadecimal* or just “hex.” This is especially true when we are dealing with individual bits of an integer.

We use the letters a, b, c, d, e, and f for the extra digits. Thus, counting in hex goes like this: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, f, 10, 11, ...

To make it clear when we are writing in hex, we prefix the number with 0x. Here is the same number and byte expressed using hex:

# Figure 33.2  One byte representing the hex number 0x3c

0x80 0x40 0x20 0x10 0x8 0x4 0x2 0x1
| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 |
0x20 + 0x10 + 0x8 + 0x4 = 0x3c

Note that one byte can always be described as a two-digit hex number (like 3c). This makes hex a reasonable way to look at binary data. A tough-guy programmer thing to say is “I reversed engineered the file format by studying the document files in a hex editor.” Want to see a file as a list of hex-encoded bytes? In Terminal, run hexdump on the file: