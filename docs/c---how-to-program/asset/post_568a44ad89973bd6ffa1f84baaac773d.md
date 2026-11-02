
```c
7    int x;
8    int y;

10   printf("%s", "Enter a six digit integer: ");
11   scanf("%2d%d", &x, &y);

13   printf("The integers input were %d and %d\n", x, y);
14 }
```

```
Enter a six digit integer: 123456
The integers input were 12 and 3456
```

**Fig. 9.23** | Inputting data with a field width. (Part 2 of 2.)

### 9.11.8 Skipping Characters in an Input Stream

Often it's necessary to *skip* certain characters in the input stream. For example, a date could be entered as

`11-10-1999`

Each number in the date needs to be stored, but the dashes that separate the numbers can be discarded. To eliminate unnecessary characters, include them in the format control string of `scanf`; whitespace characters, such as space, newline and tab, skip all leading whitespace. For example, to discard the dashes in the input, use the statement

```c
scanf("%d-%d-%d", &month, &day, &year);
```

Although this `scanf` does eliminate the dashes in the preceding input, it's possible that the date could be entered as

`10/11/1999`

In this case, the preceding `scanf` would *not* eliminate the unnecessary characters. For this reason, `scanf` provides the assignment suppression character `*`. This character enables `scanf` to read any type of data from the input and discard it without assigning it to a variable. Figure 9.24 uses the assignment suppression character in the `%*c` conversion specifier to indicate that a character appearing in the input stream should be read and discarded. Only the month, day and year are stored. The values of the variables are printed to demonstrate that the `%*c` conversion specifiers in fact can input correctly. The argument lists for each `scanf` call do not contain variables for the conversion specifiers that use the assignment suppression character. The corresponding characters are simply *discarded*.

```c
1  // Fig. 9.24: Fig09_24.c
2  // Reading and discarding characters from the input stream
3  #include <stdio.h>
4
5  int main(void)
6  {
7      int month = 0;
8      int day = 0;
9      int year = 0;
10     printf("%s", "Enter a date in the form mm-dd-yyyy: ");
11     scanf("%d%*c%d%*c%d", &month, &day, &year);
12     printf("month = %d day = %d year = %d\n", month, day, year);
13
14     printf("%s", "Enter a date in the form mm/dd/yyyy: ");
15     scanf("%d%*c%d%*c%d", &month, &day, &year);
16     printf("month = %d day = %d year = %d\n", month, day, year);
17 }
```

```
Enter a date in the form mm-dd-yyyy: 11-18-2012
month = 11 day = 18 year = 2012

Enter a date in the form mm/dd/yyyy: 11/18/2012
month = 11 day = 18 year = 2012
```

**Fig. 9.24** | Reading and discarding characters from the input stream. (Part 2 of 2.)

## 9.12 Secure C Programming

The C standard lists many cases in which using incorrect library-function arguments can result in undefined behavior. These can cause security vulnerabilities, so they should be avoided. Such problems can occur when using `printf` (or any of its variants, such as `sprintf`, `fprintf`, `printf_s`, etc.) with improperly formed conversion specifications. CERT rule FIO00-C (www.securecoding.cert.org) discusses these issues and presents a table showing the valid combinations of formatting flags, length modifiers and conversion-specifier characters that can be used to form conversion specifications. The table also shows the proper argument type for each valid conversion specification. In general, as you study any programming language, if the language specification says that doing something can lead to undefined behavior, avoid doing it to prevent security vulnerabilities.

## Summary

### Section 9.2 Streams

- All input and output is performed with streams (p. 410), which are sequences of bytes.
- Normally, the standard input stream is connected to the keyboard, and the standard output and error streams are connected to the computer screen (p. 410).
- Operating systems often allow the standard input and standard output streams to be redirected to other devices.

### Section 9.3 Formatting Output with printf

- The `0` flag (p. 421) prints leading zeros for a value that does not occupy its entire field width.

### Section 9.10 Printing Literals and Escape Sequences

Most literal characters to be printed in a `printf` statement can simply be included in the format control string. However, there are several "problem" characters, such as the quotation mark (`"`, p. 422) that delimits the format control string itself. Various control characters, such as newline and tab, must be represented by escape sequences. An escape sequence is represented by a backslash (`\`), followed by a particular escape character.

### Section 9.11 Reading Formatted Input with scanf

- Input formatting is accomplished with the `scanf` library function.
- Integers are input with `scanf` with the conversion specifiers `d` and `i` (p. 424) for optionally signed integers and `o`, `u`, `x` or `X` for unsigned integers. The modifiers `h`, `l` and `ll` are placed before an integer conversion specifier to input a short, long and long long integer, respectively.
- Floating-point values are input with `scanf` with the conversion specifiers `e`, `E`, `f`, `g` or `G`. The modifiers `l` and `L` are placed before the floating-point conversion specifiers to indicate that the input value is a `double` or `long double` value, respectively.
- Characters are input with `scanf` with the conversion specifier `c` (p. 426).
- Strings are input with `scanf` with the conversion specifier `s` (p. 426).
- A `scanf` with a scan set (p. 426) scans the characters in the input, looking only for those characters that match characters contained in the scan set. When a character is matched, it's stored in a character array. The scan set stops inputting characters when a character not contained in the scan set is encountered.
- To create an inverted scan set (p. 427), place a caret (`^`) in the square brackets before the scan characters. This causes characters input with `scanf` and not appearing in the scan set to be stored until a character contained in the inverted scan set is encountered.
- Address values are input with `scanf` with the conversion specifier `p`.
- Conversion specifier `n` stores the number of characters input so far in the current `scanf`. The corresponding argument is a pointer to `int`.
- The assignment suppression character (`*`, p. 428) reads data from the input stream and discards the data.
- A field width is used in `scanf` to read a specific number of characters from the input stream.

## Self-Review Exercises

### 9.1 Fill in the blanks in each of the following:

- a) All input and output is dealt with in the form of _______.
- b) The _______ stream is normally connected to the keyboard.
- c) The _______ stream is normally connected to the computer screen.
- d) Precise output formatting is accomplished with the _______ function.
- e) The format control string may contain _______, _______, _______, _______ and _______.
- f) The conversion specifier _______ or _______ may be used to output a signed decimal integer.
- g) The conversion specifiers _______, _______ and _______ are used to display unsigned integers in octal, decimal and hexadecimal form, respectively.
- h) The modifiers _______ and _______ are placed before the integer conversion specifiers to indicate that short or long integer values are to be displayed.
- i) The conversion specifier ______ is used to display a floating-point value in exponential notation.
- j) The modifier ______ is placed before any floating-point conversion specifier to indicate that a long double value is to be displayed.
- k) The conversion specifiers `e`, `E` and `f` are displayed with ______ digits of precision to the right of the decimal point if no precision is specified.
- l) The conversion specifiers ______ and ______ are used to print strings and characters, respectively.
- m) All strings end in the ______ character.
- n) The field width and precision in a `printf` conversion specifier can be controlled with integer expressions by substituting a(n) ______ for the field width or for the precision and placing an integer expression in the corresponding argument of the argument list.
- o) The ______ flag causes output to be left justified in a field.
- p) The ______ flag causes values to be displayed with either a plus sign or a minus sign.
- q) Precise input formatting is accomplished with the ______ function.
- r) A(n) ______ is used to scan for specific characters and store the characters in an array.
- s) The conversion specifier ______ can be used to input optionally signed octal, decimal and hexadecimal integers.
- t) The conversion specifiers ______ can be used to input a double value.
- u) The ______ is used to read data from the input stream and discard it without assigning it to a variable.
- v) A(n) ______ can be used in a `scanf` conversion specifier to indicate that a specific number of characters or digits should be read from the input stream.

### 9.2 Find the error in each of the following and explain how it can be corrected.

- a) The following statement should print the character `'e'`.

  ```c
  printf("%s\n", 'c');
  ```

- b) The following statement should print `9.375%`.

  ```c
  printf("% .3f%", 9.375);
  ```

- c) The following statement should print the first character of the string "Monday".

  ```c
  printf("%c\n", "Monday");
  ```

- d) `puts("A string in quotes");`
- e) `printf("%6d%12", 20);`
- f) `printf("\%c", '*');`
- g) `printf("%s\n", 'Richard');`

### 9.3 Write a statement for each of the following:

- a) Print 1234 right justified in a 10-digit field.
- b) Print 123.456789 in exponential notation with a sign (+ or -) and 3 digits of precision.
- c) Read a double value into variable `number`.
- d) Print 100 in octal form preceded by 0.
- e) Read a string into character array `string`.
- f) Read characters into array `n` until a nondigit character is encountered.
- g) Use integer variables `x` and `y` to specify the field width and precision used to display the double value 87.4573.
- h) Read a value of the form `3.5%`. Store the percentage in float variable `percent` and eliminate the `%` from the input stream. Do not use the assignment suppression character.
- i) Print 3.333333 as a long double value with a sign (+ or -) in a field of 20 characters with a precision of 3.
