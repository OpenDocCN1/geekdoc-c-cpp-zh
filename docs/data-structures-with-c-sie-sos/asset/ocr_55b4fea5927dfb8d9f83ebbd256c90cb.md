# Concatenation

Let S1 and S2 be strings. Recall (Sec. 3.2) that the concatenation of S1 and S2, which we denote by S1//S2, is the string consisting of the characters of S1 followed by the characters of S2.

# Example 3.6

(a) Suppose S1 = 'MARK' and S2 = 'TWAIN'. Then:
S1//S2 = 'MARKTWAIN' but S1// '[]' //S2 = 'MARK TWAIN'

(b) Concatenation is performed in C language using the strcat function, as shown below:
strcat(S1,S2); //Concatenates strings S1 and S2 and stores
the result in S1
strcat() function is part of the string.h header file; hence it must be included at the time of
pre-processing.

# Program 3.3

```
/* Code showing string concatenation in C */
#include <stdio.h>
#include <conio.h>
#include <string.h>

void main()
{
char S1[80]=("MARK");
char S2[80]=("TWAIN");
clrscr();

printf("S1 = %s",S1);
printf("\nS2 = %s",S2);
printf("\nS1//S2 = %s",strcat(S1,S2));
strcpy(S1,"MARK");
printf("\nS1//' '//S2 = %s",strcat(strcat(S1," "),S2));

getch();
}
```

Output:
S1 = MARK
S2 = TWAIN
S1//S2 = MARKTWAIN
S1//' '//S2 = MARK TWAIN

# Length

The number of characters in a string is called its length. We will write