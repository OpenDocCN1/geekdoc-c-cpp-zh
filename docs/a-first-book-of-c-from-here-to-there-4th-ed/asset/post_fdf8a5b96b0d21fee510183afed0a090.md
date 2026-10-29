
## Data Types, Declarations, and Displays

the condition is true or false. For example, in a sales application, the condition being examined might be “is the total purchase for $100 or more.” Only when this condition is true is a discount applied. Because the bool data type uses an integer storage code, however, it has useful implications that most professional C++ programmers utilize. Chapter 4 covers the practical uses of Boolean conditions, so the bool data type is discussed in more detail in that chapter.

## Determining Storage Size

A unique feature of C++ is that you can see where and how values are stored. As an example, the C++ operator `sizeof()` provides the number of bytes (discussed in Section 2.6) used to store values for the data type given in the parentheses. This built-in operator doesn’t use an arithmetic symbol to perform its operation. Program 2.1 uses this operator to determine the amount of storage reserved for the int, char, and bool data types.

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    cout << "\nData Type  Bytes";
    cout << "\n---------  -----";
    cout << "\nint        " << sizeof(int);
    cout << "\nchar       " << sizeof(char);
    cout << "\nbool       " << sizeof(bool);
    cout << '\n';

    return 0;
}
```
```

In reviewing Program 2.1, notice that the `\n` character is included at the start of each output string in the first five cout statements. Each time the compiler encounters the newline escape sequence, as part of a string or as one character, it’s translated as a single character that forces the display to start at the beginning of a new line. In the final cout statement, the newline escape sequence is inserted as a single '\n' character. Although quotation marks can be used for this final newline insertion, as "\n", doing so designates a string. The single quotes, as in '\n', clearly indicate that a single character is being transmitted. From a practical standpoint, however, both notations ("\n" and '\n') force a new line in the display.

## Point of Information

## The Character `\n` and the String "\n"

The compiler recognizes both `\n` and "\n" as containing the newline character. The difference is in the data type used. Formally, `\n` is a character literal, and "\n" is a string literal. From a practical standpoint, both cause the same thing to happen: A new line is forced in the output display. In encountering the character value `\n`, however, the compiler translates it by using the ASCII code 00001010 (see Table 2.3). In encountering the string value "\n", the compiler translates it by using the same character code but adds the code for the end-of-string character, `\0`, which is 00000000.

Good programming practice requires ending the last output display with a newline escape sequence. This practice ensures that the first line of output from one program doesn’t end up on the last line displayed by the previously executed program.

The output of Program 2.1 is compiler dependent, meaning each compiler reports the amount of storage it provides for the data type under consideration. When run on a computer using Microsoft’s current Visual C++ compiler, for example, the following output is produced:

| Data Type | Bytes |
|-----------|-------|
| int       | 4     |
| char      | 1     |
| bool      | 1     |

For this output, which is the typical storage almost all current C++ compilers provide, you can determine the range of values that can be stored in each data type. Doing so, however, requires understanding the difference between a signed and an unsigned data type, discussed in the next section.

## Signed and Unsigned Data Types

A signed data type allows storing negative values, the value 0, and positive values, so int is a signed data type. An unsigned data type provides for only non-negative values (that is, 0 and positive values). Some applications require only unsigned numerical values. For example, many date applications store dates in the numerical form yearmonthday (storing 12/25/2011 as 20111225, for example) and are concerned only with dates after 0 CE. For these applications, which never require a negative value, an unsigned data type can be used.

All unsigned integer types, such as unsigned int, provide a range of positive values that, for all practical purposes, is double the range for their signed counterparts. This extra positive range is made available by using the negative range of its signed version for additional positive numbers.

Table 2.4 lists the range of integer values supported by current C++ compilers for its signed and unsigned integer data types. As you can see, a long int uses the same amount of storage (4 bytes) as an int. The only requirement of the ANSI C++ standard is that an int must provide at least as much storage as a short int, and a long int must provide at least as much storage as an int. On early desktop computers with a memory capacity limited to thousands of bytes, a short int typically used 1 byte of storage, an int 2 bytes, and a long int 4 bytes. This storage limited the range of int values from -32,768 to +32,767 and unsigned int values from 0 to 65,535, thus doubling the number of possible positive values, which was significant. With the current range of int values in the -2 billion to +2 billion range, doubling positive values is rarely a consideration. Additionally, a long int is unnecessary now because it uses the same storage capacity as an int.

## Table 2.4 Integer Data Type Storage

| Name of Data Type | Storage Size | Range of Values |
|---|---|---|
| char | 1 | 256 characters |
| bool | 1 | true (considered as any positive value) and false (which is a 0) |
| short int | 2 | -32,768 to +32,767 |
| unsigned short int | 2 | 0 to 65,535 |
| int | 4 | -2,147,483,648 to +2,147,483,647 |
| unsigned int | 4 | 0 to 4,294,967,295 |
| long int | 4 | -2,147,483,648 to +2,147,483,647 |
| unsigned long int | 4 | 0 to 4,294,967,295 |

## Floating-Point Types

A floating-point number, more commonly known as a real number, can be the number 0 or any positive or negative number containing a decimal point. The following are examples of floating-point numbers:

```
+10.625  5.0  -6.2  3251.92  0.0  0.33  -6.67  +2.
```

Notice that the numbers 5.0, 0.0, and +2. are classified as floating-point values, but the same numbers written without a decimal point (5, 0, +2) would be integer values. As with integer values, special symbols, such as the dollar sign and comma, aren't permitted in real numbers. Examples of invalid real numbers are as follows:

```
5,326.25   24   6,459   $10.29   7,007.645
```

C++ supports three floating-point data types: float, double, and long double. The difference between these data types is the amount of storage the compiler uses for each type. Most compilers use twice the amount of storage for doubles as for floats, which allows a double to have approximately twice the precision of a float. For this reason, a float value is sometimes referred to as a single-precision number and a double value as a double-precision number. The actual storage allocation for each data type, however, depends on the compiler. The ANSI C++ standard requires only that a double have at least the same amount of precision as a float, and a long double have at least the same amount of storage as a double. Currently, most C++ compilers allocate 4 bytes for floats and 8 bytes for doubles and long doubles, which produces the range of numbers listed in Table 2.5.

## Table 2.5 Floating-Point Data Types

| Type | Storage | Absolute Range of Values (+ and -) |
|---|---|---|
| float | 4 bytes | 1.40129846432481707×10⁻⁴⁵ to 3.40282346638528860×10⁺³⁸ |
| double and long double | 8 bytes | 4.94065645841246544×10⁻³²⁴ to 1.79769313486231570×10⁺³⁰⁸ |

In compilers using the same amount of storage for double and long double numbers, these two data types are identical. (The sizeof() operator in Program 2.1 can always be used to determine the amount of storage your compiler reserves for these data types.) A float literal is indicated by appending an f or F to the number, and a long double is created by appending an l or L to the number. In the absence of these suffixes, a floating-point number defaults to a double. For example, take a look at the following:

+   9.234 indicates a double literal.
+   9.234F indicates a float literal.
+   9.234L indicates a long double literal.

The only difference in these numbers is the amount of storage the computer can use for them. Appendix D (available online) describes the binary storage format used for floating-point numbers and its impact on number precision.

## Exponential Notation

Floating-point numbers can also be written in exponential notation, which is similar to scientific notation and is commonly used to express both very large and very small values in compact form. The following examples show how numbers with decimals can be expressed in exponential and scientific notation:

| Decimal Notation | Exponential Notation | Scientific Notation |
|---|---|---|
| 162.5 | 1.625e2 | 1.625 × 10² |
| 63421. | 6.3421e4 | 6.3421 × 10⁴ |
| .00731 | 7.31e-3 | 7.31 × 10⁻³ |
| .000625 | 6.25e-4 | 6.25 × 10⁻⁴ |

In exponential notation, the letter e stands for "exponent." The number following the e represents a power of 10 and indicates the number of places the decimal point should be moved to obtain the standard decimal value. The decimal point is moved to the right if the number after the e is positive or moved to the left if the number after the e is negative. For example, the e2 in 1.625e2 means move the decimal place two places to the right, so the number becomes 162.5. The e-3 in 7.31e-3 means move the decimal point three places to the left, so 7.31e-3 becomes .00731.

Certain notations occur frequently enough in computer applications that they have their own symbols. Table 2.6 lists the most commonly used of these symbols.
