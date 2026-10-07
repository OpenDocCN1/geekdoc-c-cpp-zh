Displaying Information Onscreen 151

58 prints a new line (
n), backslash (\), the letter a, and two tabs (\t). The line ends with some descriptive text,(bell (alert)). Line 59 follows the same format.

This program prints the first two lines of Table 7.1, along with a report title and column headings. In exercise 9 at the end of this lesson, you complete this program by making it print the rest of the table.

# The printf() Conversion Specifiers

The format string must contain one conversion specifier for each printed variable.
The printf() function then displays each variable as directed by its corresponding conversion specifier. You learn more about this process in Lesson 14, "Working with the Screen, Printer, and Keyboard." For now, be sure to use the conversion specifier that corresponds to the type of variable being printed.

Exactly does this mean? If you print a variable that is a signed decimal integer (types int and long), use the %d conversion specifier. For an unsigned decimal integer (types unsigned int and unsigned long), use %u. For a floating-point variable (types float and double), use the %f specifier. The conversion specifiers you need often are listed in Table 7.2.

# TABLE 7.2 The Most Commonly Needed Conversion Specifiers

| Specifier | Meaning | Types Converted |
|---|---||
| %c | Single character | char |
| %d | Signed decimal integer | int, short |
| %ld | Signed long decimal integer | long |
| %f | Decimal floating-point number | float, double |
| %s | Character string | char arrays |
| %u | Unsigned decimal integer | unsigned int, unsigned short |
| %lu | Unsigned long decimal integer | unsigned_long |

> Any program that uses printf() should include the header stdio.h.

The literal text of a format specifier is anything that doesn't qualify as either an escape sequence or a conversion specifier. Literal text is simply printed as, including all spaces.

What about printing the values of more than one variable? A printf() statement can print an unlimited number of variables, but the format string must contain one

7