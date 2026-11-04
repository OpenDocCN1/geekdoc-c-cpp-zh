# # THE PRINTF() FUNCTION

In **Listing 1.1** you saw an example of using the `printf()` function in order to print a text string. The values of other types of variables are also printed using the `printf()` function, which uses formats to match different data types. In particular, the formats `%c`, `%d`, and `%f` specify a character, an integer, and a floating point number, respectively. In addition, there is a “family” of functions whose semantics are similar to the `printf()` function, such as the `sprintf()` function for putting data in a buffer and `fprintf()` function for printing data to a file.

C supports the following output formatting:

```
```
%d    // print as decimal integer
%6d   // print as decimal integer, at least 6 characters wide
%f    // print as floating point
%6f   // print as floating point, at least 6 characters wide
%.2f  // print as floating point, 2 characters after decimal point
%6.2f // print as floating point, at least 6 wide and 2 after decimal point
```
```

The `printf()` function also recognizes `%o` for octal, `%x` for hexadecimal, `%c` for character, `%s` for character string, and `%%` for `%` itself (numbers in octal and hexadecimal are discussed later).

**Listing 1.2** displays the contents of `IntExample.c` that illustrates how to initialize an integer-valued variable and then use the `printf()` function to display arithmetic operations on that variable.

***LISTING 1.2: IntExample.c***

```
```c
#include <stdio.h>
```
```