exert care to match the number and type of specifiers to the rest of the function arguments. For `scanf()`, remember to prefix variables’ names with the address operator (`&`).

Whitespace characters (tabs, spaces, and newlines) play a critical role in how `scanf()` views input. Except when in the `%c` mode (which reads just the next character), `scanf()` skips over whitespace characters to the first non-whitespace character when reading input. It then keeps reading characters either until encountering whitespace or until encountering a character that doesn’t fit the type being read. Let’s consider what happens if we feed the identical input line to several different `scanf()` input modes. Start with the following input line:

```
−13.45e12#  0
```

First, suppose we use the `%d` mode; `scanf()` would read the three characters (−13) and stop at the period, leaving the period as the next input character. `scanf()` then would convert the character sequence −13 into the corresponding integer value and store that value in the destination `int` variable. Next, reading the same line in the `%f` mode, `scanf()` would read the −13.45E12 characters and stop at the `#` symbol, leaving it as the next input character. It then would convert the character sequence −13.45E12 into the corresponding floating-point value and store that value in the destination `float` variable. Reading the same line in the `%s` mode, `scanf()` would read −13.45E12#, stopping at the space, leaving it as the next input character. It then would store the character codes for these 10 characters into the destination character array, appending a null character at the end. Finally, reading the same line using the `%c` specifier, `scanf()` would read and store the first character, in this case a space.

# Summary

A string is a series of characters treated as a unit. In C, strings are represented by a series of characters terminated by the null character, which is the character whose ASCII code is 0. Strings can be stored in character arrays. An array is a series of items, or elements, all of the same type. To declare an array called name that has 30 elements of type char, do the following:

```
char name[30];
```

Be sure to allot a number of elements sufficient to hold the entire string, including the null character.

String constants are represented by enclosing the string in double quotes: "This is an example of a string".

The `strlen()` function (declared in the `string.h` header file) can be used to find the length of a string (not counting the terminating null character). The `scanf()` function, when used with the `%s` specifier, can be used to read in single-word strings.

The C preprocessor searches a source code program for preprocessor directives, which begin with the `#` symbol, and acts upon them before the program is compiled. The `#include` directive causes the preprocessor to add the contents of another file to your file at the location of the directive. The `#define` directive lets you establish manifest constants—that is, symbolic