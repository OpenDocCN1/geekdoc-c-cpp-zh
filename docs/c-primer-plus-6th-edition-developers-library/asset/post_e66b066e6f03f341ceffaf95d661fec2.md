
The final two forms (\ooo and \xhh) are special representations of the ASCII code. To represent a character by its octal ASCII code, precede it with a backslash (\ ) and enclose the whole thing in single quotes. For example, if your compiler doesn’t recognize the alert character (\a), you could use the ASCII code instead:

```
beep = '\007';
```

You can omit the leading zeros, so '\07' or even '\7' will do. This notation causes numbers to be interpreted as octal, even if there is no initial 0.

Beginning with C90, C provides a third option—using a hexadecimal form for character constants. In this case, the backslash is followed by an x or X and one to three hexadecimal digits. For example, the Ctrl+P character has an ASCII hex code of 10 (16, in decimal), so it can be expressed as '\x10' or '\X010'. Figure 3.5 shows some representative integer types.

| Examples of Integer Constants |
|---|---|---|---|
| type | hexadecimal | octal | decimal |
| char | \0x41 | \0101 | N.A. |
| int | 0x41 | 0101 | 65 |
| unsigned int | 0x41u | 0101u | 65u |
| long | 0x41L | 0101L | 65L |
| unsigned long | 0x41UL | 0101UL | 65UL |
| long long | 0x41LL | 0101LL | 65LL |
| unsigned long long | 0x41ULL | 0101ULL | 65ULL |

Figure 3.5 Writing constants with the int family.

When you use ASCII code, note the difference between numbers and number characters. For example, the character 4 is represented by ASCII code value 52. The notation '4' represents the symbol 4, not the numerical value 4.

At this point, you may have three questions:

- Why aren’t the escape sequences enclosed in single quotes in the last example (printf("Gramps sez, \"a \\ is a backslash\"\n");)? When a character, be it an escape sequence or not, is part of a string of characters enclosed in double quotes, don’t enclose it in single quotes. Notice that none of the other characters in this example (G, r, a, m, p, s, and so on) are marked off by single quotes. A string of characters enclosed in double quotes is called a character string. (Chapter 4 explores strings.) Similarly, printf("Hello!\007\n"); will print Hello! and beep, but printf("Hello!7\n"); will print Hello!7. Digits that are not part of an escape sequence are treated as ordinary characters to be printed.

```
{
    int32_t me32;    // me32 a 32-bit signed variable

    me32 = 45933945;
    printf("First, assume int32_t is int: ");
    printf("me32 = %d\n", me32);
    printf("Next, let's not make any assumptions.\n");
    printf("Instead, use a \"macro\" from inttypes.h: ");
    printf("me32 = %" PRId32 "\n", me32);

    return 0;
}
```

In the final printf() argument, the PRId32 is replaced by its inttypes.h definition of "d", making the line this:

```
printf("me16 = %" "d" "\n", me16);
```

But C combines consecutive quoted strings into a single quoted string, making the line this:

```
printf("me16 = %d\n", me16);
```

Here's the output; note that the example also uses the \" escape sequence to display double quotation marks:

```
First, assume int32_t is int: me32 = 45933945
Next, let's not make any assumptions.
Instead, use a "macro" from inttypes.h: me32 = 45933945
```

It's not the purpose of this section to teach you all about expanded integer types. Rather, its main intent is to reassure you that this level of control over types is available if you need it. Reference Section VI, "Extended Integer Types," in Appendix B provides a complete rundown of the inttypes.h and stdint.h header files.

## Note C99/C11 Support

Even though C has moved to the C11 standard, compiler writers have implemented C99 features at different paces and with different priorities. At the time this book was prepared, some compilers haven't yet implemented the inttypes.h header file and features.

## Types float, double, and long double

The various integer types serve well for most software development projects. However, financial and mathematically oriented programs often make use of floating-point numbers. In C, such numbers are called type float, double, or long double. They correspond to the real types of FORTRAN and Pascal. The floating-point approach, as already mentioned, enables you to represent a much greater range of numbers, including decimal fractions. Floating-point number

C also has a double (for double precision) floating-point type. The double type has the same minimum range requirements as float, but it extends the minimum number of significant figures that can be represented to 10. Typical double representations use 64 bits instead of 32. Some systems use all 32 additional bits for the nonexponent part. This increases the number of significant figures and reduces round-off errors. Other systems use some of the bits to accommodate a larger exponent; this increases the range of numbers that can be accommodated. Either approach leads to at least 13 significant figures, more than meeting the minimum standard.

C allows for a third floating-point type: long double. The intent is to provide for even more precision than double. However, C guarantees only that long double is at least as precise as double.

## Declaring Floating-Point Variables

Floating-point variables are declared and initialized in the same manner as their integer cousins. Here are some examples:

```
float noah, jonah;
double trouble;
float planck = 6.63e-34;
long double gnp;
```

## Floating-Point Constants (Literals)

There are many choices open to you when you write a literal floating-point constant. The basic form of a floating-point literal is a signed series of digits, including a decimal point, followed by an e or E, followed by a signed exponent indicating the power of 10 used. Here are two valid floating-point constants:

```
-1.56E+12
2.87e-3
```

You can leave out positive signs. You can do without a decimal point (2E5) or an exponential part (19.28), but not both simultaneously. You can omit a fractional part (3.E16) or an integer part (.45E-6), but not both (that wouldn’t leave much!). Here are some more valid floating-point constants:

```
3.14159
.2
4e16
.8E-5
100.
```

Don’t use spaces in a floating-point constant.

```
Wrong: 1.56 E+12
```

By default, the compiler assumes floating-point constants are double precision. Suppose, for example, that some is a float variable and that you have the following statement:
some = 4.0 * 2.0;

Then 4.0 and 2.0 are stored as double, using (typically) 64 bits for each. The product is calculated using double precision arithmetic, and only then is the answer trimmed to regular float size. This ensures greater precision for your calculations, but it can slow down a program.

C enables you to override this default by using an f or F suffix to make the compiler treat a floating-point constant as type float; examples are 2.3f and 9.11E9F. An l or L suffix makes a number type long double; examples are 54.31 and 4.32e4L. Note that L is less likely to be mistaken for 1 (one) than is l. If the floating-point number has no suffix, it is type double.

Since C99, C has a new format for expressing floating-point constants. It uses a hexadecimal prefix (0x or 0X) with hexadecimal digits, a p or P instead of e or E, and an exponent that is a power of 2 instead of a power of 10. Here’s what such a number might look like:
0xa.1fp10

The a is 10 in hex, the .1f is 1/16th plus 15/256th (f is 15 in hex), and the p10 is 2^10, or 1024, making the complete value (10 + 1/16 + 15/256) x 1024, or 10364.0 in base 10 notation.

Not all C compilers have added support for this feature.

## Printing Floating-Point Values

The printf() function uses the %f format specifier to print type float and double numbers using decimal notation, and it uses %e to print them in exponential notation. If your system supports the hexadecimal format for floating-point numbers, you can use a or A instead of e or E. The long double type requires the %Lf, %Le, and %La specifiers to print that type. Note that both float and double use the %f, %e, or %a specifier for output. That’s because C automatically expands type float values to type double when they are passed as arguments to any function, such as printf(), that doesn’t explicitly prototype the argument type. Listing 3.7 illustrates these behaviors.

## Listing 3.7 The showf_pt.c Program

```
/* showf_pt.c -- displays float value in two ways */
#include <stdio.h>
int main(void)
{
    float aboat = 32000.0;
    double abet = 2.14e9;
    long double dip = 5.32e-5;

    printf("%f can be written %e\n", aboat, aboat);
    // next line requires C99 or later compliance
    printf("And it's %a in hexadecimal, powers of 2 notation\n", aboat);
```
