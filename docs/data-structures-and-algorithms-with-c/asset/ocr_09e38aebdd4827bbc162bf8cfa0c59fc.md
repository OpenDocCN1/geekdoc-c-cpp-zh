Most libraries, however, contain the strcmp() function, which compares two strings and returns a zero if two strings are identical, or a non-zero number if the strings are not the same. The syntax of strcmp() is given below:

```
strcmp(string1, string2);
```

where string1 and string2 may be string variables or string constants. The function returns a negative number if string1 is alphabetically less than the string2 and a positive number if string1 is greater than string2. More correctly, strcmp() returns the numeric difference between the first two non-matching characters.

# Example:

```
strcmp ("Newyork", "Newyork") ;
it will return zero because 2 strings are equal.
strcmp ("their", "there") ;
it will return -9 which is the numeric difference between ASCII 'i' and ASCII 'r'.
strcmp ("The", "the");
it will return -32 which is the numeric difference between ASCII 'T' and ASCII 't'.
```

# Program 3.5 : Compare two strings using strcmp() function

```
#include<stdio.h>
#include<string.h>
main()
{
    int r;
    char string1[] = "The";
    char string2[] = "the";
    r = strcmp(string1, string2);
    if(r == 0)
    printf("Strings are identical");
    else
    printf("Strings are not identical");
}
Output:
Strings are not identical
```

# String Reversal

The reverse of a string is a string with the same characters, but in the reverse order. For example, if a given string is "abcd", then the reverse of the string is "dcba". Whenever a string is the reverse of itself (e.g. madam) is called a palindrome.

# Algorithm to reverse a string

```
Algorithm: STRING_REVERSE (S)
[S is a given string]
1. Set N = Length (S)
```