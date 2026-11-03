```
while(strl[i]!='\0') /*Check for the end of first string*/
i++;
while(strl2[j]!='\0') /*Add second string at the end of first*/
{
strl[i]=strl2[j];
i++;
j++;
}
strl[i]='\0';
return strl;
```

```
char *pstrcat(char *strl,char *str2)
{
while(*strl!='\0')
strl++;
while(*str2!='\0')
{
*strl=*str2;
strl++;
strl2++;
}
*strl='\0';
return strl;
}
```

The function strcat() returns a pointer to the first string, hence it can be nested. The following program illustrates this.

```
#include<stdio.h>
#include<string.h>
main()
{
char strl[20]=\"Subhash \";
char strl2[10]=\"Chandra \";
strcat(strl,strl2);
printf(\"strl - %s\\n\",strl);
}
```

Output:
strl - Subhash Chandra Bose

Other string related functions are explained in the chapter on library functions.

# 9.4 String Pointers

We can take a char pointer and initialize it with a string constant. For example-

```
char *ptr = \"Chennai\";
```

Here ptr is a char pointer which points to the first character of the string constant “Chennai” i.e. contains the base address of this string constant.