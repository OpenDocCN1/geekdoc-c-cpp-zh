case, then the current year is not a leap year, so the variable leapyear must be set to 0 (because its value has already been set to 1 by the outer if statement).

The bottom portion of the for loop contains conditional logic that displays the appropriate message based on the value of the variable leapyear.

The output from Listing 3.3 is here:

1900: not a leap year
1953: not a leap year
1958: not a leap year
2000: leap year
2004: leap year
2006: not a leap year

# CHECKING ALPHABETIC TYPES

Letters and numbers have an ASCII value, and it's possible to check their type. Listing 3.4 displays the contents of Alphabetic.c that illustrates how to check for alphabetic characters in C.

# LISTING 3.4: Alphabetic.c

```
#include <stdio.h>
#include <ctype.h>

int main()
{
    int ch;

    for (ch = 0x7c; ch <= 0x82; ch++) {
        printf("%#04x  ", ch);

        if (isascii(ch))
        {
```