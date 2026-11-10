
## Conversions of characters and integers

There are six basic methods of converting values from one type to another. The methods are:

- **Sign extension** This technique is adopted when converting a signed object to a wider signed object, e.g. converting a short int to a long int. It preserves the numerical value by filling the extra leading space with 1’s or 0’s.
- **Zero extension** This is used when converting an unsigned object to a wider unsigned object. It works by simply prefixing the value with the relevant number of zeroes.
- **Preserve low order data-truncate** This is used when converting an object to a narrower form. Significant information may be lost.
- **Preserve bit pattern** This is used when converting between signed and unsigned objects of the same width.
- **Internal conversion** This uses special hardware to convert between floating point types and from integral to floating point types.
- **Truncate at decimal point** This is used to convert from floating point types to integral types, and may involve loss of significant information.

The basic conversions listed above are those that take place on assignment.

Conversion of a shorter integer to a longer integer preserves the sign. Traditional C uses ‘unsigned preserving integer promotion’ (unsigned short to unsigned int), while ANSI C uses ‘value preserving integer promotion’ (unsigned short to int).

A longer integer is truncated on the left when converted to a shorter integer or to a char. Excess bits are discarded.

When an unsigned integer is converted to a longer unsigned or signed integer, the value of the result is preserved. Thus, the conversion amounts to padding with zeroes on the left.

When an unsigned integer is converted to a shorter signed or unsigned integer, the value is truncated on the left. If the result is signed, this truncation may produce a negative value.

Consider the following program which illustrates the above facts:

```c
#include <stdio.h>
int main()
{
    short int si;
    long int li;
    unsigned short int usi;
    unsigned long int uli;
    si = -10;
    li = si; /* sign extension - li should be -10 */
    printf("si = %8hd li = %8ld\n",si,li);
    usi = 40000;        /* unsigned decimal constant */
    uli = usi;
                      /* zero extension - uli should be 40000 */
    printf("usi = %8hu uli = %8lu\n",usi,uli);
    uli = 0xabcdef12;   /* sets most bits */
    usi = uli;          /* will truncate - discard more
                           significant bits */
    printf("usi = %8hx uli = %8lx\n",usi,uli);
    si = usi;           /* preserves bit pattern */
    printf("si = %8hd usi = %8hu\n",si,usi);
    si = -10;
    usi = si;           /* preserves bit pattern */
    printf("si = %8hd usi = %8hu\n",si,usi);
    return 0;
}
```

**Output**

```text
si = -10     li = -10
usi = 40000  uli = 40000
usi = ef12   uli = abcdef12
si = -4334   usi = 61202
si = -10     usi = 65526
```

It may be interesting to note that the difference between the pairs of values on the last two lines is 65536. Conversions between signed long and unsigned short are typically undefined. The next program shows conversions to and from floating point types.

There is an extra complication concerning variables of type char. The conversion rules to be applied depend on whether the compiler regards char values as signed or unsigned. Basically the ANSI C standard says that variables of type char are promoted to type unsigned int or type signed int depending on whether the type char is signed or unsigned. An unsigned int may then be further converted to a signed int by bit pattern preservation. This is implementation dependent. The following program shows what might happen.

```c
#include <stdio.h>
int main()
{
    int si;
    unsigned int usi;
    char ch = 'a';
                     // Most significant bit will be zero
    si = ch;         // will give small +ve integer
    usi = ch;
    printf("c = %c\n si = %d\n usi = %u\n", ch,\
           si,usi);
    ch = '\377';     /* set all bits to 1 */
    si = ch;         /* sign extension makes negative */
    usi = ch;
    printf("si = %d\n usi = %u\n",si,usi);
    return 0;
}
```

**Output**

```text
c = a
si = 97
usi = 97
si = -1
usi = 4294967295
```

The Turbo C compiler regarded *char* as a signed data type, applying sign extension when assigning the *signed char ch* to the *signed int si*. The conversion from *signed char ch* to *unsigned int usi* is more interesting. This took place in two stages—the first being sign extension and the second being bit pattern preservation. On the IBM 6150, *char* is treated as an unsigned data type, both assignments using bit pattern preservation.

The conversion of the unsigned char to either the signed int si or the unsigned int usi is by bit pattern preservation.

### Conversions of float and double

ANSI C considers all floating point constants to be implicitly double precision, and operations involving such constants therefore take place in double precision. To force single precision arithmetic in ANSI C, use the f or F suffix on floating point constants. To force long double precision on constants, use the l or L suffix. For example, 3.14l is long double precision, 3.14 is double precision, and 3.14f is single precision in ANSI C.

What happens if you try to make a float variable exceed its limits? For example, suppose you multiply 1.0e38f by 1000.0f (overflow) or divide 1.0e-37f by 1.0e6f (underflow)? The result depends on the system. Either could cause the program to abort and to print a run-time error message. Or overflows may be replaced by a special value, such as the largest possible float value; underflows might be replaced by 0. Other systems may not issue warnings or may offer you a choice of responses. If this matter concerns you, check the rules for your system. If you cannot find the information, do not be afraid of a little trial and error.

### Conversion of floating and integral types

When a floating value is converted to an integral value, the rounded value is preserved as long as it does not overflow. When an integral value is converted to a floating value, the value is preserved unless a value of more than six significant digits is being converted to single precision, or fifteen significant digits is being converted to double precision.

Whenever a floating-point value is assigned to an integer variable in C, the decimal portion of the number gets truncated. Assigning an integer variable to a floating variable does not cause any change in the value of the number; the value is simply converted by the system and stored in the floating variable. The following program shows conversions to and from floating point types.

```c
#include <stdio.h>
int main()
{
    double  x;
    int     i;

    i = 1400;
    x = i;    /* conversion from int to double */
    printf("x = %10.6e i = %d\n",x,i);
    x = 14.999;
    i = x;    /* conversion from double to int */
    printf("x = %10.6e i = %d\n",x,i);
    x = 1.0e+60;    /* a LARGE number */
    i = x;    /* won't fit - what happens? */
    printf("x = %10.6e i = %d\n",x,i);
    return 0;
}
```

Producing the output

```text
x =  1.400000e+03 i = 1400
x =  1.499700e+01 i = 14
x =  1.000000e+60 i = 2147483647
```

The loss of significant data, a polite way of saying the answer is wrong, in the final conversion should be noted.

### 8.16.3 Casting Arithmetic Expressions

Casting an arithmetic expression tells the compiler to represent the value of the expression in a certain way. In effect, a cast is similar to a promotion, which was discussed earlier. However, a cast is under the programmer's control, not the compiler's. For example, if i is a type int, the expression

`(float)i`

casts i to float type. In other words, the program makes an internal copy of the value of i in floating point format. When is a typecast used with an arithmetic expression? The most common use is to avoid losing the fractional part of the answer in an integer division. Consider the following example.

**EXAMPLE**

20. When one integer is divided by another, any fractional part of the answer is lost.

```c
#include <stdio.h>
int main()
{
    int a = 100,b = 40;
    float c;
```
