| Conversion specifier | Description |
|---|---|
| l or L | Place before any of the floating-point conversion specifiers to indicate that a double or long double value is to be input. The corresponding argument is a pointer to a double or long double variable. |
| Characters and strings |  |
| c | Read a character. The corresponding argument is a pointer to a char; no null ('\0') is added. |
| s | Read a string. The corresponding argument is a pointer to an array of type char that's large enough to hold the string and a terminating null ('\0') character—which is automatically added. |
| Scan set [scan characters] | Scan a string for a set of characters that are stored in an array. |
| Miscellaneous |  |
| p | Read an address of the same form produced when an address is output with %p in a printf statement. |
| n | Store the number of characters input so far in this call to scanf. The corresponding argument must be a pointer to an int. |
| % | Skip a percent sign (%) in the input. |

Fig. 9.17 | Conversion specifiers for scanf. (Part 2 of 2.)

# 9.11.3 Reading Integers with scanf

Figure 9.18 reads integers with the various integer conversion specifiers and displays the integers as decimal numbers. Conversion specifier %i can input decimal, octal and hexadecimal integers.

```
```c
// Fig. 9.18: fig09_18.c
// Reading input with integer conversion specifiers
#include <stdio.h>

int main(void)
{
    int a;
    int b;
    int c;
    int d;
    int e;
    int f;
    int g;

    puts("Enter seven integers: ");
    scanf("%d%d%d%o%u%x%X", &a, &b, &c, &d, &e, &f, &g);
    puts("\nThe input displayed as decimal integers is:");
```
```

Fig. 9.18 | Reading input with integer conversion specifiers. (Part 1 of 2.)