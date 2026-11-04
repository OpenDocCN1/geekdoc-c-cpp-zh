The output from Listing 6.5 is here:

Initial Values:
1 2 3 4 5
Updated Values:
3 6 9 12 15

# A FOR LOOP WITH POINTERS TO NUMBERS

Listing 6.6 displays the contents of Palindromes1.c that illustrates how to determine whether a string is a palindrome. In case you have forgotten, a palindrome is a number or string that is a "mirror image" of itself, such as 12321, "rotor," and "radar," whereas 1231 and "rattan" are not palindromes.

# **LISTING 6.6: Palindromes1.c**

```
```c
#include <stdio.h>
#include <stdio.h>
#include <string.h>

int scanString(char str[])
{
    int result = 0;
    char *ptr;
    int len = strlen(str);

    for(int i=0; i<len/2; i++)
    {
        if(str[i] != str[len-i-1])
        {
            result = 1;
            break;
        }
    }
```
```