# ### Solution 3.19

Figure 3.34 shows the program listing (Program: cpy.c). The program forms string John-Smith and displays it on the screen.

```
~~~c
/*--------------------------------------------------------
                  strcpy and strcat

   This program is an example use of the strcpy and strcat

   Author: Dogan Ibrahim
   File  : cpy.c
   Date  : December 2020
----------------------------------------------------------*/

#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main(void)
{
   char a[]="John";
   char b[] = "Smith";
   char c[] = "-";
   char d[BUFSIZ];


   //
   // Using strcpy
   //
   strcpy(d, a);                       // d=John
   strcat(d, c);                       // d=John-
   strcat(d, b);                       // d=John-Smith
   printf("My name is %s\n", d);

   return 0;
}
~~~
```

Figure 3.34 Program cpy.c

The program displays the following text:

My name is John-Smith

# ### 3.2.12 • Character macros

Several useful macros are available that can be used to test various characters. The header file <ctype.h> must be included at the beginning of the program before these macros can be used.