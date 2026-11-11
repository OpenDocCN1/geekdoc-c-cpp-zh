```
```c
{
char first[80], second[80];
int value;
clrscr();
printf(”Enter a string: ”);
gets(first);
printf(”Enter another string: ”);
gets(second);
value = strcmp(first, second);
if(value == 0)
puts(”The two strings are equal”);
else if(value < 0)
puts(”The first string is smaller ”);
else if(value > 0)
puts(”the first string is bigger”);
getch();
}
```
```

The output of the above code is as follows:
Enter a string: MANISH
Enter another string: VARSHNEY
The first string is smaller

# strcmp( ) Function

This function is same as strcmp () which compares 2 strings but not case sensitive.

# Example

strcmpi(”THE”,”the”); will return 0.

# Problem

Write a program to input two strings and print the appropriate message that the strings are alphabetically equal or not whether the strings are not case sensitive.

# Solution

```
```c
#include <stdio.h>
#include <conio.h>
#include <string.h>
void main()
{
    char s[80],s1[80];
    clrscr();
    printf(”\n enter first string”);
    scanf(”%s”,s);
    printf(”\n enter second string”);
    scanf(”%s”,s1);
    if(strcmpi(s,s1)==0)
    printf(”\n both the strings are alphabetically equal”);
```
```

```
```c
else
printf(”\n both the strings are not alphabetically equal”);
getch ();
}
```
```

The output of the above code is as follows:
Enter first string Manish
Enter second string MANISH
Both the strings are alphabetically equal.

# strcat ( ) Function

The strcat function is used to join one string to another. It takes two strings as arguments; the characters of the second string will be appended to the first string.
The general syntax of strcat ( ) function is as follows:
strcat (str1, str2);
Where str1 and str2 are two string arguments, string str2 is appended to string str1.

# Problem

Write a program to read two strings and append the second string to the first string.

# Solution

```
```c
#include <stdio.h>
#include <string.h>
#include <conio.h>
void main()
{
char first[80], second[80];
clrscr();
printf(”Enter a string:”);
gets (first);
printf(”Enter another string: ”);
gets (second);
strcat(first, second);
printf(”\n the concatenated string is %s\n”, first);
getch();
}
```
```

The output of the above code is as follows
Enter a string: Manish
Enter another string: Varshney
The concatenated string is Manish Varshney

# strlwr ( ) Function

The strlwr function converts upper case characters of string to lower case characters.
The general syntax is as follows:
strlwr (str1);