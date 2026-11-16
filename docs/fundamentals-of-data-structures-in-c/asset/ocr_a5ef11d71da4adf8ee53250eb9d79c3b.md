# 1.16.1 The strlen() function

The strlen() (string length) function returns the count of number of characters stored in a string. The general form or the syntax of strlen() function is

```
x = strlen(str);
```

where x is an integer variable which receives the length of the string and sr is a valid string variable or a constant. Program 1.17 helps you to understand things better.

# Program 1.17 :

```
/* strlen.c */
#include<stdio.h>
#include<string.h>
void main()
{
char str[25];
printf("Enter a string : ");
gets(str);
printf("The length of the string is %d", strlen(str));
}
```

The program displays the following output

```
Enter a string : Surya
The length of the string is 5
```

In Program 1.17 the strlen() function takes a single argument (i.e., the string entered by the user), and returns the length of the string. Note that the length of the string doesn't count the null character. If a string with spaces is entered by the user the strlen() function returns the length of the string including the number of spaces in between the string. For example,

```
Enter a string : Raj Kumar
The length of the string is 9
```

The strlen() function also counts the space in between the string and returns the length of the string as 9.

# 1.16.2 The strcpy() function

A string cannot be copied directly using an assignment statement (with the exception of pointers). However, it is possible to copy a string element by element using assignment statements. The strcpy() (string copy) function is used to copy the contents of one string to another. The general form or the syntax of strcpy() function is

```
strcpy(string1, string2);
```

where string1 and string2 are valid string variables or string constants. The strcpy() function takes two arguments for copying. The string in the second argument