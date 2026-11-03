strstr(), strtok() and strxfrm(). Let's look at some cases. In the expression memchar(const *s, int c, size_t m); the function searches for the character c among the first n characters of the content pointed to by *s variable. The statement char *strcat(char s, const char p); concatenate the string p at the end of the string s. The strcmp() function compares two alphanumeric arguments, strcpy() copies the string of the first argument in the second, strncpy() does the same thing for the first n characters and strlen() provides the size of a string. The strcoll() and strxfrm() functions compare strings of different languages. They are not in Turbo C or in Microsoft C.

The example-program below illustrates the use of some alphanumeric functions.

# Example-program #9A

```
/* Programa "Alphanum.cpp" */
#include <stdio.h>
#include <string.h>
#define TOTAL 80
void Invert(char s[])
{ int i, k=strlen(s);
printf("\n");
for(i=k-1; i>=0; --i) putchar(s[i]);
}
void Space(char s[])
{ int i,k=strlen(s);
printf("\n");
for(i=0;i<k;i++){putchar(s[i]); putchar(' ');}
}
main()
{ char s[TOTAL]; char m[TOTAL];
char p[]="Bed"; char q[]="time";
printf("\n Type a name:\n"); gets(s);
Invert(s); printf("\n");
Space(s); printf("\n");
printf("\n% s",p); printf("\n% s",q);
strcpy(m,p); strcat(m,q); printf("\n% s\n",m);
}
```