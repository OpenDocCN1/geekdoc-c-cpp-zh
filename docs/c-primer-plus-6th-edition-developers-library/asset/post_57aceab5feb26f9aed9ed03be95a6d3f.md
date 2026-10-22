
```c
scanf("%*d %*d %d", &n);
printf("The last integer was %d\n", n);

return 0;
}
```

The `scanf()` instruction in Listing 4.17 says, "Skip two integers and copy the third into n." Here is a sample run:

```
Please enter three integers:
2013 2014 2015
The last integer was 2015
```

This skipping facility is useful if, for example, a program needs to read a particular column of a file that has data arranged in uniform columns.

## Usage Tips for printf()

Specifying fixed field widths is useful when you want to print columns of data. Because the default field width is just the width of the number, the repeated use of, say,

```
printf("%d %d %d\n", val1, val2, val3);
```

produces ragged columns if the numbers in a column have different sizes. For example, the output could look like the following:

```
12 234 1222
4 5 23
22334 2322 10001
```

(This assumes that the value of the variables has been changed between print statements.)

The output can be cleaned up by using a sufficiently large fixed field width. For example, using

```
printf("%9d %9d %9d\n", val1, val2, val3);
```

```
printf("Count Beppo ran %.2f miles in 3 hours.\n", distance);
```

might produce

```
Count Beppo ran 10.22 miles in 3 hours.
```

Changing the conversion specification to `%10.2f` would give you the following:

```
Count Beppo ran      10.22 miles in 3 hours.
```

## Locale Choices

The United States and many other parts of the world use a period to separate the integer part of a decimal value from the fractional part, as in 3.14159. But many other parts of the world use a comma instead, as in 3,14159. You may have noticed that the `printf()` and `scanf()` specifiers don't seem to offer the comma format. But C hasn't ignored the rest of the world. As outlined in Appendix B, Section V, "The Standard ANSI C Library with C99 Additions," C supports the concept of a locale. This gives a C program the option of choosing a particular locale. For example, it might specify a Netherlands locale, and `printf()` and `scanf()` would use the local convention (a comma, in this case) when displaying and reading floating-point values. Also, once you specified that environment, you would use the comma convention for numbers appearing in your code:

```
double pi = 3,14159;  // Netherlands locale
```

The C standard requires but two locales: "C" and "". By default, programs use the "C" locale which, basically, is U.S. usage. The "" locale stands for a local locale in use on your system. In principle, it could be the same as the "C" locale. In practice, operating systems such as Unix, Linux, and Windows offer long lists of locale choices. However, they might not offer the same lists.

## Key Concepts

The C char type represents a single character. To represent a sequence of characters, C uses the character string. One form of string is the character constant, in which the characters are enclosed in double quotation marks; "Good luck, my friend" is an example. You can store a string in a character array, which consists of adjacent bytes in memory. Character strings, whether expressed as a character constant or stored in a character array, are terminated by a hidden character called the null character.

It’s a good idea to represent numerical constants in a program symbolically, either by using `#define` or the keyword `const`. Symbolic constants make a program more readable and easier to maintain and modify.

The standard C input and output functions `scanf()` and `printf()` use a system in which you have to match type specifiers in the first argument to values in the subsequent arguments. Matching, say, an int specifier such as `%d` to a float value produces odd results. You have to exert care to match the number and type of specifiers to the rest of the function arguments. For `scanf()`, remember to prefix variables' names with the address operator (`&`).

Whitespace characters (tabs, spaces, and newlines) play a critical role in how `scanf()` views input. Except when in the `%c` mode (which reads just the next character), `scanf()` skips over whitespace characters to the first non-whitespace character when reading input. It then keeps reading characters either until encountering whitespace or until encountering a character that doesn't fit the type being read. Let's consider what happens if we feed the identical input line to several different `scanf()` input modes. Start with the following input line:

```
 -13.45e12# 0
```

First, suppose we use the `%d` mode; `scanf()` would read the three characters (-13) and stop at the period, leaving the period as the next input character. `scanf()` then would convert the character sequence -13 into the corresponding integer value and store that value in the destination `int` variable. Next, reading the same line in the `%f` mode, `scanf()` would read the -13.45E12 characters and stop at the `#` symbol, leaving it as the next input character. It then would convert the character sequence -13.45E12 into the corresponding floating-point value and store that value in the destination `float` variable. Reading the same line in the `%s` mode, `scanf()` would read -13.45E12#, stopping at the space, leaving it as the next input character. It then would store the character codes for these 10 characters into the destination character array, appending a null character at the end. Finally, reading the same line using the `%c` specifier, `scanf()` would read and store the first character, in this case a space.

## Summary

A string is a series of characters treated as a unit. In C, strings are represented by a series of characters terminated by the null character, which is the character whose ASCII code is 0. Strings can be stored in character arrays. An array is a series of items, or elements, all of the same type. To declare an array called name that has 30 elements of type char, do the following:

```
char name[30];
```

Be sure to allot a number of elements sufficient to hold the entire string, including the null character.

String constants are represented by enclosing the string in double quotes: "This is an example of a string".

The `strlen()` function (declared in the `string.h` header file) can be used to find the length of a string (not counting the terminating null character). The `scanf()` function, when used with the `%s` specifier, can be used to read in single-word strings.

The C preprocessor searches a source code program for preprocessor directives, which begin with the `#` symbol, and acts upon them before the program is compiled. The `#include` directive causes the preprocessor to add the contents of another file to your file at the location of the directive. The `#define` directive lets you establish manifest constants—that is, symbolic

```c
printf("Please enter your first name.");
scanf("%s", name);
printf("All right, %c, what's your age?\n", name);
scanf("%f", age);
xp = age + X;
printf("That's a %s! You must be at least %d.\n", B, xp);
return 0;
}
```

5. Suppose a program starts as follows:

```
#define BOOK "War and Peace"
int main(void)
{
    float cost =12.99;
    float percent = 80.0;
```

Construct a `printf()` statement that uses BOOK, cost, and percent to print the following:

```
This copy of "War and Peace" sells for $12.99.
That is 80% of list.
```

6. What conversion specification would you use to print each of the following?

- a. A decimal integer with a field width equal to the number of digits
- b. A hexadecimal integer in the form 8A in a field width of 4
- c. A floating-point number in the form 232.346 with a field width of 10
- d. A floating-point number in the form 2.33e+002 with a field width of 12
- e. A string left-justified in a field of width 30

7. Which conversion specification would you use to print each of the following?

- a. An unsigned long integer in a field width of 15
- b. A hexadecimal integer in the form 0x8a in a field width of 4
- c. A floating-point number in the form 2.33E+02 that is left-justified in a field width of 12
- d. A floating-point number in the form +232.346 in a field width of 10
- e. The first eight characters of a string in a field eight characters wide
