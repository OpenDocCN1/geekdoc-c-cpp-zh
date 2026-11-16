(i.e., string2) is copied to the first argument (i.e., string1). For copying one string into another the base address of the source and target strings should be supplied to this function. Program 1.18 helps you to understand things better.

# Program 1.18 :

```
/* strcpy.c */
#include<stdio.h>
#include<string.h>
void main()
{
char str[25];
char cpy[25];
printf("Enter a string : ");
gets(str);
strcpy(cpy, str);
printf("\n The source string is %s", str);
printf("\n The copied string is %s", cpy);
}
```

The program displays the following output
Enter a string : Krishna
The source string is Krishna
The copied string is Krishna

In Program 1.18 the variable str is used to read the string as input and it copies the input string to cpy. The variable in str is copied to cpy, character by character until it encounters the NULL character. The NULL character is also copied.

# 1.16.3 The strcat( ) function.

The strcat( ) (string concatenate) function concatenates the source string at the end of the target string. The strcat( ) function takes two arguments for concatenating. The string in the second argument (i.e., string2) is concatenated with the string present in the first argument (i.e., string1). The general form or the syntax of strcat( ) function is

```
strcat(string1, string2);
```

where string1 and string2 are valid string variables or string constants. The content of string2 is concatenated with the content of string1. Program 1.19 helps you to understand things better.