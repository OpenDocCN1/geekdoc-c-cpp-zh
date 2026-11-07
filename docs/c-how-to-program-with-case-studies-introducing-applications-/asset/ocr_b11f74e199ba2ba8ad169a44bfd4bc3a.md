The statement

reads a string from the keyboard into `string2`. You pass the array name to `scanf` without the `&` used with non-string variables. The `&` is normally used to provide `scanf` with a variable’s *location* in memory so that a value can be stored there. In Section 6.7, when we discuss passing arrays to functions, we’ll discuss why the `&` is not necessary for array names.

```
scanf("%19s", string2);
```

It’s your responsibility to ensure that the array into which the string is read is capable of holding any string that the user types at the keyboard. Function `scanf` does *not* check how large the array is. It will read characters until a *space*, *tab*, *newline* or *end-of-file indicator* is encountered. The string `string2` should be no longer than 19 characters to leave room for the terminating null character. If the user types 20 or more characters, your program may crash or create a security vulnerability called a buffer overflow. For this reason, we used the conversion specification `%19s`. This tells `scanf` to read a maximum of 19 characters, preventing it from writing characters into memory beyond the end of `string2`. (In Section 6.13, we revisit the potential security issue raised by inputting into a character array and discuss the C standard’s `scanf_s` function.)

# ### 6.5.5 Outputting a Character Array That Represents a String

A character array representing a string can be output with `printf` using the `%s` conversion specification. For example, you can print the character array `string2` with

```
printf("%s\n", string2);
```

Like `scanf`, `printf` does not check how large the character array is. It displays the string’s characters until it encounters a terminating null character. [Consider what would print if, for some reason, the terminating null character were missing.]

# ### 6.5.6 Demonstrating Character Arrays

Figure 6.8 demonstrates initializing a character array with a string literal, reading a string into a character array, printing a character array as a string and accessing a string’s individual characters. The program uses a `for` statement (lines 20–22) to loop through the `string1` array and print the individual characters separated by spaces, using the `%c` conversion specification. The condition in the `for` statement is true while the counter is less than the array’s size and the terminating null character has not been encountered in the string. This program reads only strings that do not contain whitespace characters. We’ll show how to read strings containing whitespace characters in Chapter 8.

```
```c
// fig06_08.c
// Treating character arrays as strings.
#include <stdio.h>
#define SIZE 20
```
```

**Fig. 6.8**  Treating character arrays as strings. (Part I of 2.)