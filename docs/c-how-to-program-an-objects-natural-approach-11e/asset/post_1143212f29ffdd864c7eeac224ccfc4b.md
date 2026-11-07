
Initial principal: 1000.00  
Interest rate: 0.05

| Year | Amount on deposit |
|---:|---:|
| 1 | 1050.00 |
| 2 | 1102.50 |
| 3 | 1157.63 |
| 4 | 1215.51 |
| 5 | 1276.28 |
| 6 | 1340.10 |
| 7 | 1407.10 |
| 8 | 1477.46 |
| 9 | 1551.33 |
| 10 | 1628.89 |

**Fig. 4.4** | Compound-interest calculations with `for`. (Part 2 of 2.)

### Formatting the Principal and Interest Rate

Figure 4.3 introduced C++20’s `format` function. In that example’s format string, we used one empty placeholder (`{}`) to insert a variable’s value at the placeholder’s position in the string. In Fig. 4.4, lines 12–13 format the `principal` and `rate` values using placeholders that concisely specify formatting instructions. The formatted results are shown in the first two lines of Fig. 4.4’s output.

Each format call in lines 12–13 uses the placeholder:

```cpp
{:>7.2f}
```

The colon (`:`) introduces a format specifier indicating how to format the corresponding value. In the format specifier `>7.2f`:

- `>7` says the value should be right-aligned (`>`) in a field width of 7 character positions, and
- `.2f` says we’re formatting a floating-point number (`f`) with two digits of precision (`.2`) to the right of the decimal point.

The value of `principal` (1000.00) requires exactly seven characters to display, including the decimal point, so it fills the entire 7 character positions. However, `rate`’s value (0.05) requires only four total character positions, so it will be right-aligned in the 7 character positions and filled from the left with leading spaces, as in the following diagram:

![](img/7b5e2088e71c7f78681d4ddbcf104c06_213_0.png)

Numeric values are right-aligned by default, so the `>` is not required here. You also can left-align numeric values in a field width via `<`. If we were to do that here for `0.05`, the value would be formatted with three trailing spaces.

### Formatting the "Year" and "Amount on Deposit" Column Heads

In line 16’s format string `"\n{:<20}\n"` the string "Year" is simply placed at the first placeholder’s position—that placeholder, `{}`, does not specify any formatting.

The placeholder `{:>20}` indicates that its corresponding argument, the 17-character string "Amount on Deposit", should be right-aligned (`>`) in a field of 20 characters. So, `format` inserts three leading spaces to right-align the 17-character string in the 20-character field. Strings are left-aligned by default, so the `>` is required here to force right alignment. If the string to display has more characters than the specified field width, the field width expands to accommodate all the characters.

### Performing the Interest Calculations with Standard Library Function pow

The `for` statement (lines 19–25) iterates 10 times, varying the `int` control variable `year` from 1 to 10 in increments of 1. Variable `year` represents *n* in the problem statement. C++ does not include an exponentiation operator, so we use the standard library function `pow` (line 21) from the header `<cmath>` (line 5)—`pow(x, y)` calculates *x* raised to the *y*th power. The function receives two `double` arguments and returns a `double` value. Line 21 performs the calculation *a* = *p*(1 + *r*)ⁿ, where *a* is amount, *p* is principal, *r* is rate, and *n* is year.

Function `pow`’s first argument—the calculation `1.0 + r`—produces the same result each time through the loop, so repeating it in every iteration of the loop is wasteful. Many of today’s optimizing compilers place such calculations before loops in the compiled code to improve program performance.

![](img/7b5e2088e71c7f78681d4ddbcf104c06_214_0.png)

### Formatting the Year and Amount-on-Deposit Values in the for Loop

Line 24’s format string uses two placeholders to format the year and amount values:

```cpp
"{:>4d}{:>20.2f}\n"
```

- The placeholder `{:>4d}` indicates that `year`’s value should be formatted as an integer (`d` means decimal integer) right-aligned (`>`) in a field of width 4. This right-aligns all the year values under the four-character "Year" column.
- The placeholder `{:>20.2f}` formats `amount`’s value right-aligned (`>`) in a field width of 20 as a floating-point number with two digits to the right of the decimal point (`.2f`). Formatting the amounts this way aligns their decimal points vertically, as is typical with monetary amounts. The field width of 20 right-aligns the amounts under the column heading "Amount on Deposit".

### Floating-Point Number Precision and Memory Requirements

A `float` represents a single-precision floating-point number. Most of today’s systems store these in four bytes of memory with approximately seven significant digits. A `double` represents a double-precision floating-point number. Most of today’s systems store these in eight bytes of memory with approximately 15 significant digits—approximately double the precision of floats. Most programmers use type `double`. C++ treats floating-point numbers such as 3.14159 in a program’s source code as `double` values by default. Such values in the source code are known as floating-point literals. The C++ standard requires only that type `double` provide at least as much precision as `float`. There is also type `long double`, which provides at least as much precision as `double`.⁴

4. “Fundamental types,” Accessed April 14, 2023. https://en.cppreference.com/w/cpp/language/types. This page shows all the C++ fundamental types and their typical ranges.

### Floating-Point Numbers Are Approximations

In conventional arithmetic, floating-point numbers often arise as a result of division. Dividing 10 by 3, the result is 3.3333333..., with the sequence of 3s repeating infinitely. The computer allocates a fixed amount of space to hold such a value, so the stored value can be only an approximation. Floating-point types, like `double`, suffer from what is referred to as *representational error*. Assuming that floating-point numbers are represented exactly (e.g., using them in comparisons for equality) can lead to incorrect results.

Floating-point numbers have numerous applications, especially for measured values. For example, when we speak of a “normal” body temperature of 98.6 degrees Fahrenheit, we do not need to be precise to a large number of digits. When we read the temperature on a thermometer as 98.6, it actually might be 98.594732103. Calling this number 98.6 is fine for most body temperature calculations. Generally, `double` is preferred over `float` because doubles represent floating-point numbers more precisely.<sup>5</sup>

### A Warning about Displaying Rounded Values

This example declared `double` variables `amount`, `principal` and `rate` to be of type `double`. Unfortunately, floating-point numbers can cause trouble with fractional monetary amounts. Here’s a simple explanation of what can go wrong when floating-point numbers are used to represent monetary amounts displayed with two digits to the right of the decimal point. Two calculated monetary amounts stored in the machine could be 14.234 (rounded to 14.23 for display purposes) and 18.673 (rounded to 18.67 for display purposes). When these amounts are added, they produce the internal sum 32.907, which would typically be rounded to 32.91 for display purposes. Thus, your output could appear as

```text
      14.23
    + 18.67
    -------
      32.91
```

but a person adding the individual numbers as displayed would expect the sum to be 32.90. You’ve been warned!

### Even Common Monetary Amounts Can Have Floating-Point Representational Errors

Even simple monetary amounts stored as doubles can have representational errors. To see this, we created a simple program that defined the variable `d` as follows:

```cpp
double d{123.02};
```

We displayed `d`’s value with 20 digits of precision to the right of the decimal point. The resulting output showed 123.02 as 123.0199999..., which is another example of a representational error. Though some monetary amounts can be represented precisely as doubles, many cannot. In Section 4.14’s Objects Natural Case Study, we represent monetary amounts precisely with the Boost Multiprecision library.

### Checkpoint

- 1. *(Fill-In)* A field width specifies the _______ to use when displaying a value.
  - **Answer:** number of character positions.

5. Typically, the standard floating-point representation is IEEE 754 (https://en.wikipedia.org/wiki/IEEE_754).
