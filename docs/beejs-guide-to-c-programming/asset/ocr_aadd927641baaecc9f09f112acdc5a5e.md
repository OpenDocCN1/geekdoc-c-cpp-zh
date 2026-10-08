# Chapter 37. Fixed Width Integer Types

To this, we can take advantage of a fact about C that you might have forgotten: adjacent string literals are automatically concatenated to a single string. E.g.:

```
printf("Hello, %world\n");    // Prints "Hello, world!"
```

And these macros are string literals, we can use them like so:

```
#include <stdio.h>
#include <stdint.h>
#include <intypes.h>

int main(void)
{
    int_least16_t x = 3490;
    printf("The value is %%%PRIDLEAST16 \!\n", x);
}
```

We also have a pile of macros for printing unsigned types:

| PRIon | PRIOLEASTn | PRIOFastn | PRIOMAX |
| PRIun | PRILEASTn | PRIUFastn | PRIuMAX |
| PRIxn | PRILEXASTn | PRIXastn | PRIXMAX |
| PRIxn | PRILEXASTn | PRIFXastn | PRIxMAX |

In this case, o, u, x, and X correspond to the documented format specifiers in printf().

And, as before, the lowercase should be substituted with 8, 16, 32, or 64.

But just when you think you had enough of macros, it turns out we have a complete complementary set of them for scanf(!).

| SCndn | SCDLEASTn | SCGFastn | SCNMAX |
| SCnIn | SCNLEASTn | SCNFastn | SCNIMAX |
| SCnOn | SCNLEASTn | SCGFastn | SCNMAX |
| SCUn | SCUFEASTn | SCUFastn | SCuMAX |
| SCxn | SCXLEASTn | SCFXastn | SCxMAX |

Remember: when you want to print out a fixed size integer type with printf() or scanf(), grab the corresponding format specifier from <intypes.h>.