# **Solution 3.36**

Figure 3.64 shows the program listing (Program: **convupper.c**). Function **UpperCase** receives the address of the string and converts it to upper case by calling the built-in function **toupper**. The string is then displayed by the main program as follows:

MY RASPBERRY PI COMPUTER

```
```c
/*------------------------------------------------------------------
   CONVERT A STRING TO UPPER CASE
   ==============================

   This program converts a given string to upper case using pointers

   Author: Dogan Ibrahim
   File  : convupper.c
   Date  : December 2020
-------------------------------------------------------------------*/
#include <stdio.h>
#include <ctype.h>

void UpperCase(char *s)
{
    while(*s != '\0')
    {
        *s = toupper(*s);
        ++s;
    }
}

int main(void)
{
    char MyString[] = "my Raspberry Pi computer";
    UpperCase(MyString);
    printf("%s\n", MyString);

    return 0;
}
```
```

Figure 3.64 Program convupper.c

# **Arrays of pointers**

A common use of an array of pointers is with strings. Here, each entry in the array is a string and is pointed to by the array indexes. As an example, consider the following array of pointers: