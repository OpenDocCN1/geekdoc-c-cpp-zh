# AN INTRODUCTION TO C AND PROGRAMMING

That's a lot shorter! Note the #include <string.h> at the start, which tells the compiler we want to use functions from the string library.

This shows two string functions strcpy (string copy) copies the string at the second argument to the start of the first argument strcat (string concatenate) does the same thing, but instead of copying to the start of the first argument, it finds the terminating zero of the first argument and starts copying to its location, thus joining the two strings together.

# OVERWRITE

It looks like it is possible to use strcpy and strcat to copy part of a string itself - strcpy (a+1, a) for example. Dont try! The source and destination buffers for strcpy and strcat must be completely separate areas of memory, if not the

# Comparing strings

Another requirement is to be able to compare two strings to see if they are the same. As we've already seen, we can compare numeric values with the == operator, but this doesn't work with strings. Remember that the name of a string is really just a pointer to a location in memory containing the string, so using == to compare two strings will only tell you if they're at the same place in memory, not if two strings at different locations are the same.

You can use == to compare two char variables, and a string is an array of chars, so it's possible to write a simple piece of code that compares each character in a string in turn:

```
#include <stdio.h>

void main (void)
{
    char str1[10] = "first";
    char str2[10] = "fire";
    char *ptr1 = str1, *ptr2 = str2;

    while (*ptr1 != 0 && *ptr2 != 0)
    {
        if (*ptr1 != *ptr2)
        {
            break;
        }
        ptr1++;
```