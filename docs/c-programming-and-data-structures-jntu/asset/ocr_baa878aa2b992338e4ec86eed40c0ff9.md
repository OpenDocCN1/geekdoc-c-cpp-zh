# xxxii The C99 Standard

New type long long (signed and unsigned), at least 64 bits wide.

> Note: It seems that these type specifiers may occur in any order, e.g., _Complex double long or signed long int long would be legal.

The implementation of the complex types is defined by the standard to use cartesian coordinates (real and imaginary part), i.e. forbids the use of polar coordinates (distance from [0,0] and an angle). Furthermore, the same paragraph also specifies that a complex type has the same alignment requirements as an array of two elements of the corresponding floating types, the first must be the real part and the second the imaginary part.

Objects of the new boolean type _Bool may have one of the two values zero or one.

# Format Modifiers for Printf() Added by C99

C99 adds several format modifiers to printf(): hh, ll, j, z, and t. The hh modifier can be applied to d, i, o, u, x, or n. It specifies that the corresponding argument is a signed or unsigned char value or, in the case of n, a pointer to a signed char variable. The ll modifier also can be applied to d, i, o, u, x, or n. It specifies that the corresponding argument is a signed or unsigned long long int value or, in the case of n, a pointer to a long long int. C99 also allows the l to be applied to the floating-point specifiers a, A, e, E, f, g, and G, but it has no effect. The j format modifier, which applies to d, i, o, u, x, X, or n, specifies that the matching argument is of type intmax_t or uintmax_t. These types are declared in <stdint.h> and specify greatest-width integers. The z format modifier, which applies to d, i, o, u, x, X, or n, specifies that the matching argument is of type size_t. This type is declared in <stddef.h> and specifies the result of sizeof. The t format modifier, which applies to d, i, o, u, x, X, or n, specifies that the matching argument is of type ptrdiff_t. This type is declared in <stddef.h> and specifies the difference between two pointers.

```
#include <stdio.h>
int main(void)
{
/* This prints "this is a test" left justified
in 20 character field.
*/
printf("%-20s", "this is a test");
/* This prints a float with 3 decimal places in a 10
character field. The output will be " 12.235".
*/
printf("%10.3f", 12.234657);
return 0;
}
```

# Changes to the Integer Promotion Rules

C99 enhances the integer promotion rules. In C89, a value of type char, short int, or an int bit-field can be used in place of an int or unsigned int in the expression. If the promoted value can be held in an int, the promotion is made to int; otherwise, the original value is promoted to unsigned int.