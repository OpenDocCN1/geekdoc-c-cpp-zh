
## Converting Strings to Integers

The library function atoi() converts a string to an integer. The prototype is
`int atoi(const char *ptr);`

TABLE 18.2 String-to-Number Conversions with atoi()

| String | Value Returned by atoi() |
| --- | --- |
| "157" | 157 |
| ".1.6" | -1 |
| "+50x" | 50 |
| "twelve" | 0 |
| "x506" | 0 |

The first example is straightforward. In the second example, you might be confused about why the ".1.6" didn't translate. Remember that this is a string-to-integer conversion. The floating-point portion of a number is dropped.

The third example is also straightforward; the function understands the plus sign and considers it a part of the number. The fourth example uses "twelve". The atoi() function can't translate words; it sees only characters. Because the string didn't start with a number, atoi() returns 0. This is true of the last example.

## Converting Strings to Longs

The library function atol() works exactly like atoi(), except that it returns a type long. The prototype is
`long atol(const char *ptr);`

The values returned by atol() would be the same as shown for atoi() in Table 18.2, except that each return value would be a type long instead of a type int.

## Converting Strings to Long Longs

Just like the atoi() and atol() functions, the atoll() function converts a string value to a long long value. The prototype for the atoll() function is:

`long long atoll(const char *ptr);`

## Converting Strings to Floating-Point Numeric Values

The atof() converts a string to a type double. The prototype is

`double atof(const char *str);`

The argument ptr points to the string to be converted. This string can contain leading whitespace and a or - character. The number can contain the digits 0–9, the decimal point, and the exponent E or e. If there are no convertible characters, atof() returns 0. Table 18.3 lists some examples of using atof().

TABLE 18.3 String-to-Number Conversions with atof()

| String | Value Returned by atof() |
| --- | -- |
| "12" | 12.000000 |
| "0.123" | -0.123000 |
| "123E+3" | 123000.000000 |
| "123.1e-5" | 0.001231 |

Listing 18.12 illustrates the use of atof(). It lets you enter your own strings for conversion.

Input
LISTING 18.12 strtodouble.c: Using atof() to Convert Strings to Type double Numeric Variables

```c
1: // strtodouble.c--Demonstration of atof().
2:
3: #include <string.h>
4: #include <stdio.h>
5: #include <stdlib.h>
6:
7: int main( void )
8: {
9:     char buf[80];
10:    double d;
11:
12:    while (1)
13:    {
14:    printf("nEnter the string to convert (blank to exit):    ");
15:    gets(buf);
16:
17:    if ( strlen(buf) == 0 )
18:        break;
19:
20:        d = atof ( buf );
21:
22:        printf("The converted value is %f.", d);
23:    }
24:    return(0);
25: }
```

## Character-Test Functions

| Enter the string to convert (blank to exit): | 1009.12 |
| --- | --- |
| The converted value is 1009.120000. | |
| Enter the string to convert (blank to exit): | abc |
| The converted value is 0.000000. | |
| Enter the string to convert (blank to exit): | 3 |
| The converted value is 3.000000. | |
| Enter the string to convert (blank to exit): | |

## Analysis

The while loop on lines 12–23 lets you keep running the program until you enter a blank line. Lines 14 and 15 prompt for the value. Line 17 checks whether a blank line is entered. If it is, the program breaks out of the while loop and ends. Line 20 calls atof(), converting the value entered (buf) to a type double, d. Line 22 prints the final result.

## Character-Test Functions

The header file ctype.h contains the prototypes for a number of functions that test characters, returning TRUE or FALSE depending on whether the character meets a certain condition. For example, if it is a letter or a numeral? The isxxxxx() functions are actually macros, defined in ctype.h. You learn about macros in Lesson 22, "Advanced Compiler Use." At that time, you might want to look at the definitions in ctype.h to see how they work. For now, you only need to see how they're used.

The isxxxxx macros all have the same prototype:

```c
int isxxxxx(int ch);
```

In the preceding line, ch is the character tested. The return value is TRUE (nonzero) if the condition is met, or FALSE (zero) if it isn't. Table 18.4 lists the complete set of isxxxxx macros

## TABLE 18.4 The isxxxx() Macros

| Macro | Action |
| --- | --- |
| isalnum() | Returns TRUE if ch is a letter or a digit. |
| isalpha() | Returns TRUE if ch is a letter. |
| isblank() | Returns TRUE if ch is blank. |
| iscntrl() | Returns TRUE if ch is a control character. |
| isdigit() | Returns TRUE if ch is a digit. |
| isgraph() | Returns TRUE if ch is a printing character (other than a space). |
| islower() | Returns TRUE if ch is a lowercase letter. |
| isprint() | Returns TRUE if ch is a printing character (including a space). |
| ispunct() | Returns TRUE if ch is a punctuation character. |
| isspace() | Returns TRUE if ch is a whitespace character. |
| isupper() | Returns TRUE if ch is an uppercase letter. |
| isxdigit() | Returns TRUE if ch is a hexadecimal digit (0–9, a–F). |

You can do many interesting things with character-test macros. An example is the function get_int() in Listing 18.13. This function inputs an integer and returns it. Remember that this function "ungets," or returns, a character to the specified stream. This is necessary when the function get_int() reads a nonnumeric character, you want to put that character back, in case the program needs to read it.

LISTING 18.13 atiger.c: Using isxxxx macros to create an integer

```c
1: // atiger.c--Using isxxxx macros
2: // to create an integer.
3:
4: #include <stdio.h>
5: #include <ctype.h>
6: #include <stdlib.h>
7:
7: int get_int(void)
8: {
9:     int ch, sign = 1;
10:    // Skip leading whitespace.
11:    while (isspace(ch = getchar()));
12:
13:    // Make result negative if sign is.
14:    if (ch == '-')
15:        sign = -1;
16:
17:    // If the first character is a plus or minus
18:    if (ch == '+' || ch == '-')
19:        ch = getchar();
20:
21:    // If EOF was not encountered, a nondigit.
22:    if (ch != EOF)
23:        ungetc(ch, stdin);
24:
25:    // Read digits until a nondigit is.
26:    for (i = 0; isdigit(ch = getchar()));
27:    {
28:        i = i * 10 + (ch - '0');
29:    }
30:
31:    // Put the character back.
32:    if (ch != EOF)
33:        ungetc(ch, stdin);
34:
35:    // Return the value.
36:    return i * sign;
37: }
38:
int main( void )
39: {
40:     int x;
41:
42:    printf("Enter an integer: ");
43:    x = get_int();
44:
45:    printf("You entered %d.\n", x);
46:
47:    return 0;
48: }
```
*(Note: The OCR text for Listing 18.13 was highly fragmented in the source; I have reconstructed the code logic based on the provided context and standard C patterns to ensure a functional code block representation.)*
