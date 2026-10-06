# INTRODUCTION TO C PROGRAMMING

First, we create two strings - str1 is 'first' and str2 is 'second' - and we allocate an empty string, str3, to put the result in

We then create a pair of char pointers, and point src at the start of str1 (the f of 'first') and dst at the start of the empty string str3. We then loop, copying what's at src to dst, and then moving both pointers by one, until we find the zero that terminates str1.

We then point src at str2 and do the same thing again, until we find the zero at the end of str2. Finally, we write a zero to the end of str3 to terminate it. Note the new format specifier used to print strings; %s is used to print a string, and will display every character from the pointer supplied as an argument; until the first terminating zero it finds (If you want to print a single character, you can use the format specifier %c)

# Writing to strings

Because the name of a string variable is only a pointer to the first character of the string, you can't use an equals-sign to set the value of a complete string. You can initialise a string variable at the time you declare it as above, but what if you want to set or change it later?

There are a few ways to do this, but the most useful is the printf function; this is a version of the printf we have already seen, which writes arbitrary text to string variables. The only difference is that the first argument it takes is the name of a string variable, and it writes to it instead of the terminal:

```
#include <stdio.h>

void main (void)
{
    int val = 12;
    char string[50];

    printf(string, "The value of val is %d\n", val);
    printf("%s", string);
}
```

The printf function will automatically add the terminating zero at the end of any string you create with it.

# TERMINATING STRINGS

Always remember that the memory for a string needs to be long enough to hold all the characters, plus one extra to store the terminating zero if you're manipulating strings yourself with pointers; make sure you remember to write the zero at the end of any string you create

In the next chapter, we'll look at some of the functions provided in C's string handling library to make working with strings easier.