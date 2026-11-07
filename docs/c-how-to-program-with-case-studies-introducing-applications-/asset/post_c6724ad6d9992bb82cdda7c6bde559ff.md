
such as the quotation mark (") that delimits the format control string itself. Various control characters, such as newline and tab, must be represented by escape sequences. An escape sequence is represented by a backslash (\), followed by a particular escape character. The following table lists the escape sequences and the actions they cause.

| Escape sequence | Description |
|---|---|
| \' (single quote) | Output the single quote (') character. |
| \" (double quote) | Output the double quote (") character. |
| \? (question mark) | Output the question mark (?) character. |
| \\ (backslash) | Output the backslash (\) character. |
| \a (alert or bell) | Cause an audible (bell) or visual alert (typically, flashing the window in which the program is running). |
| \b (backspace) | Move the cursor back one position on the current line. |
| \f (new page or form feed) | Move the cursor to the next logical page's start. |
| \n (newline) | Move the cursor to the beginning of the next line. |
| \r (carriage return) | Move the cursor to the beginning of the current line. |
| \t (horizontal tab) | Move the cursor to the next horizontal tab position. |
| \v (vertical tab) | Move the cursor to the next vertical tab position. |

## Self Check

1 (Multiple Choice) Which of the following statements a), b) or c) is false?
a) Literal characters included in the format control string are ignored by printf.
b) Various control characters, such as newline and tab, must be represented by escape sequences.
c) An escape sequence is represented by a backslash (\), followed by a particular escape character.
d) All of the above statements are true.
Answer: a) is false. Actually, printf displays any literal characters included in the format control string.

2 (Multiple Choice) Which escape sequence is described by "Cause an audible (bell) or visual alert (typically, flashing the window in which the program is running)"?
a) \b.
b) \r.
c) \a.
d) \v.
Answer: \a.

## 9.11 Formatted Input with scanf

Precise input formatting can be accomplished with scanf. Every scanf statement contains a format control string that describes the format of the data to be input. The format control string consists of conversion specifiers and literal characters. Function `scanf` has the following input formatting capabilities:

- 1. Inputting all types of data.
- 2. Inputting specific characters from an input stream.
- 3. Skipping specific characters in the input stream.

### 9.11.1 scanf Syntax

Function scanf is written in the following form:

```
scanf(format-control-string, other-arguments);
```

The *format-control-string* describes the input formats, and *other-arguments* are pointers to variables in which the inputs will be stored.

When inputting data, prompt the user for one data item or a few data items at a time. Avoid asking the user to enter many data items in response to a single prompt. Always consider what the user and your program will do when incorrect data is entered—for example, a value for an integer that’s nonsensical in a program’s context, or a string with missing punctuation or spaces.

### 9.11.2 scanf Conversion Specifiers

The following table summarizes the conversion specifiers used to input all types of data. Note that the `d` and `i` conversion specifiers have different meanings for input with scanf, but are interchangeable for output with printf.

| Conversion specifier | Description |
|---|---|
| **Integers** | |
| `d` | Read an optionally signed decimal integer. The corresponding argument is a pointer to an `int`. |
| `i` | Read an optionally signed decimal, octal or hexadecimal integer. The corresponding argument is a pointer to an `int`. |
| `o` | Read an octal integer. The corresponding argument is a pointer to an unsigned `int`. |
| `u` | Read an unsigned decimal integer. The corresponding argument is a pointer to an unsigned `int`. |
| `x` or `X` | Read a hexadecimal integer. The corresponding argument is a pointer to an unsigned `int`. |
| `h`, `l` and `ll` | Place before any integer conversion specifier to indicate that a short, long or long long integer is to be input. |
| **Floating-point numbers** | |
| `e`, `E`, `f`, `F`, `g` or `G` | Read a floating-point value. The corresponding argument is a pointer to a floating-point variable. |
| `l` or `L` | Place before any floating-point conversion specifier to indicate that a double or long double value is to be input. The corresponding argument is a pointer to a double or long double variable. |
| **Characters and strings** | |
| `c` | Read a character. The corresponding argument is a pointer to a char; no null (`'\0'`) is added. |
| `s` | Read a string. The corresponding argument is a pointer to an array of type char that's large enough to hold the string and a terminating null (`'\0'`) character—which is automatically added. |
| **Scan set** | |
| `%[scan characters]` | Scan a string for a set of characters that are stored in an array. |
| **Miscellaneous** | |
| `p` | Read an address of the same form produced when an address is output with `%p` in a printf statement. |
| `n` | Store the number of characters input so far in this call to scanf. The corresponding argument must be a pointer to an int. |
| `%` | Skip a percent sign (%) in the input. |

### 9.11.3 Reading Integers

Figure 9.12 reads integers with the various integer conversion specifiers and displays the integers as decimal numbers. Conversion specification %i can input decimal, octal and hexadecimal integers.

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

**Fig. 9.12** | Reading input with integer conversion specifiers. (Part 1 of 2.)

Enter seven integers:
-70 -70 070 0x70 70 70 70

The input displayed as decimal integers is:
-70 56 112 56 70 112

Fig. 9.12 | Reading input with integer conversion specifiers. (Part 2 of 2.)

### 9.11.4 Reading Floating-Point Numbers

When inputting floating-point numbers, any of the floating-point conversion specifiers e, E, f, g or G can be used. Figure 9.13 reads three floating-point numbers, one with each of the three types of floating conversion specifiers, and displays all three numbers with conversion specifier f.

```
// fig09_13.c
// Reading input with floating-point conversion specifiers
#include <stdio.h>

int main(void) {
    double a = 0.0;
    double b = 0.0;
    double c = 0.0;

    puts("Enter three floating-point numbers:");
    scanf("%le%lf%lg", &a, &b, &c);

    puts("\nUser input displayed in plain floating-point notation:");
    printf("%f\n%f\n%f\n", a, b, c);
}
```

Enter three floating-point numbers:
1.27987 1.27987e+03 3.38476e-06

User input displayed in plain floating-point notation:
1.279870
1279.870000
0.000003

Fig. 9.13 | Reading input with floating-point conversion specifiers.

### 9.11.5 Reading Characters and Strings

Characters and strings are input using the conversion specifiers c and s, respectively. Figure 9.14 prompts the user to enter a string. The program inputs the first character of the string with %c and stores it in the character variable x, then inputs the remainder of the string with %s and stores it in character array y.

```c
// fig09_14.c
// Reading characters and strings
#include <stdio.h>

int main(void) {
    char x = '\0';
    char y[9] = "";

    printf("%s", "Enter a string: ");
    scanf("%c%8s", &x, y);

    printf("The input was '%c' and \"%s\"\n", x, y);
}
```

```
Enter a string: Sunday
The input was 'S' and "unday"
```

**Fig. 9.14** | Reading characters and strings.

### 9.11.6 Using Scan Sets

A sequence of characters can be input using a scan set—a set of characters enclosed in square brackets, [], and preceded by a percent sign in the format control string. A scan set scans the characters in the input stream, looking only for those characters that match characters contained in the scan set. Each time a character is matched, it’s stored in the scan set’s corresponding character array argument. The scan set stops inputting characters when scanf encounters a character not contained in the scan set. If the first character in the input stream does not match a character in the scan set, scanf does not modify its corresponding array argument. Figure 9.15 uses the scan set [aeiou] to scan the input stream for vowels. For our input "qeeaoeah", the first seven letters are input. The eighth letter (h) is not in the scan set, so scanf stops scanning for characters.

```c
// fig09_15.c
// Using a scan set
#include <stdio.h>

int main(void) {
    char z[9] = "";

    printf("%s", "Enter string: ");
    scanf("%8[aeiou]", z); // search for set of characters

    printf("The input was \"%s\"\n", z);
}
```

**Fig. 9.15** | Using a scan set. (Part 1 of 2.)
