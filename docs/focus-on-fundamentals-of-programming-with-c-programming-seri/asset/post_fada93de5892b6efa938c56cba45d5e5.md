
Your program should be run and produce output on the following data:

```
10, 98, 234, 567, 999, 5432, 9999
```

Note that this lab has nothing to do with factorials and the multiplication of numbers. By this I mean that I am not looking for a cleaner or more efficient approach to calculating factorials. The goal of this lab is to manipulate linear linked lists using dynamic storage allocation! You are required to implement the algorithm specified.

Output from your program should be sent to the terminal window (your screen) as well as the requested `csis.txt` output file. Be sure to read the document on Capturing Program Output. Your full name must appear as a comment in the source file that contains `main()`. Be sure to include the `csis.txt` output file in your zip archive.

## Chapter 21. Bitwise Operators

- Introduction to Bitwise Operators
- Bitwise And
- Masks
- WordStar
- Bitwise Or
- Bitwise Exclusive-Or
- Bitwise Negate
- Left Shift Operator
- Right Shift Operator
- Rotate Example
- Extracting Bit Fields
- Bitwise Operator Homework
- Bitwise Operator Lab

### Introduction to Bitwise Operators

C provides a host of operators specifically designed for performing operations on individual bits:

| `&` | bit-and |
| `` `|` `` | bit-or |
| `^` | bit-exclusive or |
| `~` | bit-negate (one's complement) |
| `<<` | left shift |
| `>>` | right shift |

All bitwise operators except the bit-negate are binary operators and therefore take two operands. Bit operations can be performed on any type of integer value in C, such as:

```
int             unsigned int
short           unsigned short
long            unsigned long
char            unsigned char
```

but not on:

```
float
double
long double
```

The bitwise operators are applied in parallel to the individual bit positions within each operand. This is unlike logical operators that treat each operand as one single zero (false) or non-zero (true) value.

### Bitwise And

Similar to the logical AND operator (`&&`), the bitwise-and operator (`&`) produces a true value only if both operands are true (i.e., have non-zero values).

| b1 | b2 | b1 & b2 |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

We assume a 16-bit integer:

```
// and1.c

#include <stdio.h>

int main(void) {
    int x = 0x2719;   // 0010 0111 0001 1001
    int y = 0x35CD;   // 0011 0101 1100 1101
    int z;

    z = x & y;        // 0010 0101 0000 1001
    printf("z = 0x%x\n", z);
    return 0;
}
```

The output of this program is:

```
z = 0x2509
```

Note that each of the corresponding bits within each `int` variable are bit-anded together.

Here's another example:

```
// and2.c

#include <stdio.h>

int main(void) {
    int x = 0x1234;    // 0001 0010 0011 0100
    int y = 0x3468;    // 0011 0100 0110 1000
    int z = 0x5248;    // 0101 0010 0100 1000

    printf("0x%x\n", x & x);
    printf("0x%x\n", x & y);
    printf("0x%x\n", x & y & z);
    printf("0x%x\n", x & 1);
    return 0;
}
```

In the first printf() statement, any quantity bit-anded with itself returns itself as a value:

```
x = 0x1234 = 0001 0010 0011 0100
x = 0x1234 = 0001 0010 0011 0100
---------------------------------
0001 0010 0011 0100 = 0x1234
```

In the second printf() statement, variables x and y are bit-anded together producing:

```
x = 0x1234 = 0001 0010 0011 0100
y = 0x3468 = 0011 0100 0110 1000
---------------------------------
0001 0000 0010 0000 = 0x1020
```

In the third printf() statement, all three variables x, y, and z are bit-anded together producing:

```
x = 0x1234 = 0001 0010 0011 0100
y = 0x3468 = 0011 0100 0110 1000
z = 0x5248 = 0101 0010 0100 1000
---------------------------------
0001 0000 0000 0000 = 0x1000
```

The fourth printf() statement has the effect of extracting the rightmost bit of x, either a 0 or a 1.

```
x = 0x1234 = 0001 0010 0011 0100
0x0001 = 0000 0000 0000 0001
                    0000 0000 0000 0000 = 0x0
```

Note that this is a good test to see whether x is odd or even:

```
printf("%s", x & 1 ? "Odd" : "Even");
```

Keep in mind the distinction between the bitwise-and operator (&) and the logical-and operator (&&):

```
// and3.c
#include <stdio.h>
int main(void) {
    int x = 1;
    int y = 2;
    printf("bitwise = %d   logical = %d\n", x & y, x && y);
    return 0;
}
```

The output produced looks like this:

```
bitwise = 0   logical = 1
```

### Masks

Bitwise ANDing is frequently used for masking operations. A *mask* is a constant or variable that is used to extract desired bits in a variable or expression. A mask can be used to set specific bits of a data item to 0. In the example below, we'll preserve the rightmost two bits from x and zero (mask) out all of the other bits:

```
// mask1.c

#include <stdio.h>

int main(void) {
    int x = 0x0679;    // 0000 0110 0111 1001
    int mask = 0x0003; // 0000 0000 0000 0011

    x = x & mask;      // 0000 0000 0000 0001
    printf("x = %x\n", x);
    return 0;
}
```

The output produced is:

```
x = 0x1
```

Note that we could have written:

```
x &= mask;
```

Now suppose we want to set all but the rightmost four bits of a word to 0:

```
// mask2.c
#include <stdio.h>
int main(void) {
    int x = 0x1234; // 0001 0010 0011 0100
    int mask = 0x000F; // 0000 0000 0000 1111
    x &= mask; // 0000 0000 0000 0100
    printf("x = 0x%x\n", x);
    return 0;
}
```

The output produced is:

```
x = 0x4
```

We can also use a mask to determine the low-order bit of an int expression:

```
// mask3.c
#include <stdio.h>
int main(void) {
    int i;
    int mask = 0x0001; // 0000 0000 0000 0001
    for (i = 0; i < 10; i++) {
        printf("%d ", i & mask);
    }
    return 0;
}
```

The above program prints an alternating sequence of 0's and 1's:

```
0 1 0 1 0 1 0 1 0 1
```

If we wished to find the value of a particular bit within an expression, we can use a mask that is 1 in that position and 0 elsewhere. For example, we can check the 5th bit from the right of an int:

```
// mask4.c
#include <stdio.h>
int main(void) {
    int x = 0x1234;    // 0001 0010 0011 0100
    int mask = 0x0010; // 0000 0000 0001 0000
    if (x & mask) {
        printf("Bit is a 1.");
    } else {
        printf("Bit is a 0.");
    }
    return 0;
}
```

The output produced is:

```
Bit is a 1.
```

### WordStar

WordStar was a word processor application that had a dominant market share during the early-to-mid 1980s. It used the high-order bit of an ASCII character for special formatting purposes.

WordStar would set the high order bit on the last character of a word to flag the location it can insert spaces to justify the right margin. It also set the high order bit on the spaces it inserts to know which spaces it can remove when it justifies the text. For example, it wouldn't want to remove the double space you put at the end of a sentence.

If you were to use a simple text editor to output the characters in a file created by WordStar, it might look something like this:

```
6$t WritA . functio$ calle$ find_$trinA tO determine$ iF on$t characteU$ c strinA$ exi$tUr in$ideA another$^ string$F TnA fir$ur^ argumen$t tOr^ thA$ c functio$ $hou$t bA thA characteU$ $trinA thaD tO tO bA $earches$ an$ thA$ c $econ$t argumeU$ thA$ $trinA wA ara interes$ed^ iOr finding$&r 1$t^ thA$ c functio$ findU thA $pecific $tring'+ 'theo havA 10 returU thA locatioU c 10 thA $ourcA $trinA wherA thA $trinA waU found$& 1F thA functio$ doeU c not find the $tring, then have it return -1. (25)
```

In fact, this is a question from an exam that I created with WordStar in 1986. I recently came across the file and wanted to view its contents. The reason for all of the gobbledeygook is due to the fact that WordStar has set the high order bit on many of the characters. Keep in mind that ASCII is actually a 7-bit code and never used the high-order bit to define a character. WordStar used this high order bit for its own purposes!

We can create a program that reads the file one character at a time. The program creates a mask to turn off the high-order bit before outputting the character:

```
putchar(c & 0x7f);
```

This statement bit-ands the character with the mask 01111111, which effectively turns off the high-order bit.
