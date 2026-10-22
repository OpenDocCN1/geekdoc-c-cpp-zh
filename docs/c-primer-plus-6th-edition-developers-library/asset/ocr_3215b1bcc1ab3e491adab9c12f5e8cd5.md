# What Does a Conversion Specification Convert?

Let’s take a closer look at what a conversion specification converts. It converts a value stored in the computer in some binary format to a series of characters (a string) to be displayed. For example, the number 76 may be stored internally as binary 01001100. The %d conversion specifier converts this to the characters 7 and 6, displaying 76. The %x conversion converts the same value (01001100) to the hexadecimal representation 4c. The %c converts the same value to the character representation L.

The term conversion is probably somewhat misleading because it might suggest that the original value is replaced with a converted value. Conversion specifications are really translation specifications; %d means “translate the given value to a decimal integer text representation and print the representation.”

# Mismatched Conversions

Naturally, you should match the conversion specification to the type of value being printed. Often, you have choices. For instance, if you want to print a type int value, you can use %d, %x, or %o. All these specifiers assume that you are printing a type int value; they merely provide different representations of the value. Similarly, you can use %f, %e, or %g to represent a type double value.

What if you mismatch the conversion specification to the type? You’ve seen in the preceding chapter that mismatches can cause problems. This is a very important point to keep in mind, so Listing 4.11 shows some more examples of mismatches within the integer family.

# Listing 4.11 The intconv.c Program

```
/* intconv.c -- some mismatched integer conversions */
#include <stdio.h>
#define PAGES 336
#define WORDS 65618
int main(void)
{
    short num = PAGES;
    short mnum = -PAGES;

    printf("num as short and unsigned short: %hd %hu\n", num, num);
    printf("-num as short and unsigned short: %hd %hu\n", mnum, mnum);
    printf("num as int and char: %d %c\n", num, num);
    printf("WORDS as int, short, and char: %d %hd %c\n", WORDS, WORDS, WORDS);
    return 0;
}
```