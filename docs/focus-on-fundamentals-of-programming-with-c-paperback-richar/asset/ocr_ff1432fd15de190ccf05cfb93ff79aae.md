# # Char Data Type

Each character is stored in 1 byte (8-bits) according to its ASCII code and is considered to have the corresponding integer value (0 – 255). Characters are written between single quotes and can be:

+   - uppercase letters: ('A' ... 'Z')
+   - lowercase letters: ('a' ... 'z')
+   - digits: ('0' ... '9')
+   - punctuation: ('.', ',', '!', '?', ';', ':', etc.)
+   - special characters ('*', '+', '-', '/', '%')
+   - white space characters ('blank', tab, newline)

C is best described as a somewhat weakly-typed language and thus can blur the distinction among data types. For example, we can add characters as if they were integers:

```
printf("%5d", 'A' + 'B' + 'C');
```

This outputs the sum of the ASCII values as 198.

Here's some code to print all the characters in a machine's character set, showing the decimal, hexadecimal, and character values. Note that the character sequence \t represents a tab. Please enter this code into your C compiler and execute the program:

```
// ascii.c

#include <stdio.h>

int main(void) {
    int i;

    for (i = 0; i < 128; i++) {
        printf("%4d\t %4x\t %4c\n", i, i, i);
    }
    return 0;
}
```