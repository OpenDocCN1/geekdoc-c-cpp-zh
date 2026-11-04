the `char` type is signed or unsigned. It depends on the compiler; thus, if it is significant for your program, you should explicitly write `signed char` or `unsigned char` instead of `char`. Printable characters are always positive. The other types are signed by default. In signed types, the leftmost bit is reserved for the sign; it is 1 if the number is negative, 0 otherwise. The advantage of using unsigned types is that they have a higher upper limit than their signed counterparts, since they don't need to account for negative values.

The `float`, `double`, and `long double` types are used to store values with a fractional part, that is, floating-point numbers. Unlike integer types, floating-point types are always signed. The C standard does not specify the number of the precision digits since different computers may use different formats to store floating-point numbers. Typically, the default precision of the `float` type is 6 digits after the decimal point, while the precision of the `double` type is 15 digits. The range of the `long double` type isn't shown in Table 2.1 because its length varies, with 10 and 16 bytes being the most common sizes. It may also have the same size as of `double`. Although the `long double` type supports the highest precision, it is rarely used because the precision of the `float` and `double` types is usually sufficient.

Although C types may come in different sizes, the C standard requires that the `long` type must not be smaller than `int`, which must not be smaller than `short`. Similarly, `long double` must not be smaller than `double`, which must not be smaller than `float`. The size of the `short` and `int` types must be 16 bits at least, while the `long` type must be 32 bits at least. If the `short` type meets your needs and the available memory is limited, it'd be better to use it instead of the `int` type, because its size is usually smaller. Information about the integer and floating types in the local implementation is provided in the `limits.h` and `float.h` files, respectively.

*For simplicity, we've made some assumptions throughout this book. We assume that the type characteristics are those shown in Table 2.1, that one byte is eight bits wide, and the system uses the most common method to represent signed numbers, that is, the two's complement. Also, we assume that the underlying character set is the American Standard Code for Information Interchange (ASCII) set.*

> If you don't care about precision, use the `float` type, because it usually reserves fewer bytes and calculations with `float` numbers tend to be executed faster.

Consider the following program. Although we haven't discussed yet about `if` and `printf()`, we think that you can get the idea. The `==` operator compares the values. So, tell us, what does the following program output?

```
```c
#include <stdio.h>
int main(void)
{
    float a = 3.1;

    if (a == 3.1)
        printf("Yes\n");
    else
        printf("No\n");

    printf("%.9f\n", a-3.1);
    return 0;
}
```
```