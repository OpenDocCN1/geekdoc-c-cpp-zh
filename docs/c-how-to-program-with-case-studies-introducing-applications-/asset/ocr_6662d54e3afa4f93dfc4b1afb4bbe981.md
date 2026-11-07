| Conversion specifier | Description |
|---|---|
| 1 or L | Place before any floating-point conversion specifier to indicate that a double or long double value is to be input. The corresponding argument is a pointer to a double or long double variable. |
| **Characters and strings** | |
| c | Read a character. The corresponding argument is a pointer to a char; no null (`'\0'`) is added. |
| s | Read a string. The corresponding argument is a pointer to an array of type char that's large enough to hold the string and a terminating null (`'\0'`) character—which is automatically added. |
| **Scan set** | |
| *[scan characters]* | Scan a string for a set of characters that are stored in an array. |
| **Miscellaneous** | |
| p | Read an address of the same form produced when an address is output with `%p` in a printf statement. |
| n | Store the number of characters input so far in this call to scanf. The corresponding argument must be a pointer to an int. |
| % | Skip a percent sign (%) in the input. |

# 9.11.3 Reading Integers

Figure 9.12 reads integers with the various integer conversion specifiers and displays the integers as decimal numbers. Conversion specification %i can input decimal, octal and hexadecimal integers.

```
```c
// fig09_12.c
// Reading input with integer conversion specifiers
#include <stdio.h>

int main(void) {
    int a = 0;
    int b = 0;
    int c = 0;
    int d = 0;
    int e = 0;
    int f = 0;
    int g = 0;

    puts("Enter seven integers: ");
    scanf("%d%i%i%i%o%u%x", &a, &b, &c, &d, &e, &f, &g);

    puts("\nThe input displayed as decimal integers is:");
    printf("%d %d %d %d %d %d %d\n", a, b, c, d, e, f, g);
}
```
```

**Fig. 9.12** | Reading input with integer conversion specifiers. (Part 1 of 2.)