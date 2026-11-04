Count:  1

String: California
Char:  z
Count:  0

# # CONVERTING STRINGS TO DECIMAL VALUES

This section contains an example of built-in functions in C that enable you to test the characters in a string to determine whether they are digits.

# ***LISTING 4.9: DisplayDigits.c***

```
```c
#include <ctype.h>
#include <stdio.h>

void checkDigits(char str[])
{
    printf("Number: %s\n",str);

    for(int i=0; str[i]; i++)
    {
        if(isdigit(str[i]))
        {
            printf("Digit: %c\n",str[i]);
        }
        else
        {
            printf("Not Digit: %c\n",str[i]);
        }
    }

    printf("\n");
}
```
```