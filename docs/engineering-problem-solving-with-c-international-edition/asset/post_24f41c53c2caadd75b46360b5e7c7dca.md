
## Type specifiers

### System dependent

The type specifiers for signed integers are short, int, and long, for short integer, integer, and long integer, respectively. The specific ranges of values are system dependent, which means that the ranges can vary from one system to another. In the last section of this chapter, we present a program that you can use to determine the ranges of the numeric data types on your system. On many systems, the short integer and the integer data types range from -32,768 to 32,767, and the long integer type often represents values from -2,147,483,648 to 2,147,483,647. (The unusual limits such as 32,767 and 2,147,483,647 relate to conversions of binary values to decimal values.) C also allows an unsigned qualifier to be added to integer specifiers, where an unsigned integer represents only positive values. Signed and unsigned integers can represent the same number of values, but the ranges are different. For example, if an unsigned short has the range of values from 0 to 65,535, then a short has the range of values from -32,768 to 32,767; both variables can represent a total of 65,536 values.

The type specifiers for floating-point values are float (single precision), double (double precision), and long double (extended precision). The following statement from program chapter1_1 thus defines seven variables that all contain double-precision floating-point values:

```
double x1=1, y1=5, x2=4, y2=7,
side_1, side_2, distance;
```

The difference between the float, double, and long double types relates to the precision (or accuracy) and the range of the values represented. The precision and range are system dependent. Table 2.2 contains precision and range information for integers and floating-point values used by the Microsoft Visual C++ compiler that can be used to run C programs, as well as C++ programs. (C++ is an extension of C.) A program given in Section 2.10 allows you to obtain this information for your computer system. On most systems, a double data type stores about twice as many decimal digits of precision as are stored with a float data type.

Table 2.2 Example Data-Type Limits*

| | Integers |
|---|---|
| short | Maximum = 32,767 |
| int | Maximum = 2,147,483,647 |
| long | Maximum = 2,147,483,647 |
| | Floating Point |
| float | 6 digits of precision<br>Maximum exponent 38<br>Maximum value 3.402823e+38 |
| double | 15 digits of precision<br>Maximum exponent 308<br>Maximum value 1.797693e+308 |
| long double | 15 digits of precision<br>Maximum exponent 308<br>Maximum value 1.797693e+308 |

*Microsoft Visual C++ 2010 Express compiler.

In addition, a double value will have a wider range of exponent values than a float value. The long double value may have more precision and a still wider exponent range, but this is again system-dependent. A floating-point constant such as 2.3 is assumed to be a double constant. To specify a float constant or a long double constant, the letter (or suffix) F or L must be appended to the constant. Thus, 2.3F and 2.3L represent a float constant and a long double constant, respectively.

## Character Data

- Characters
- Binary code
- ASCII
- EBCDIC

Character data is an important type of information to represent and to manipulate in engineering programming problems. In order to work with characters, we need to understand more about their representation in the computer's memory. Recall that all information stored in a computer is represented internally as sequences of binary digits (0 and 1). Each character corresponds to a binary code value. The most commonly used binary codes are ASCII (American Standard Code for Information Interchange) and EBCDIC (Extended Binary Coded Decimal Interchange Code). In the discussions that follow, we assume that ASCII code is used to represent characters. Table 2.3 contains a few characters, their binary form in ASCII, and the integer values that correspond to the binary values. The character 'a' is represented by the binary value 1100001, which is equivalent to the integer value of 97. A total of 128 characters can be represented in the ASCII code. A complete ASCII code table is given in Appendix B.

Character data can be represented by constants or by variables. A character constant is enclosed in single quotes, such as 'A', 'b', and '3'. A variable that is going to contain a character is defined as an integer or as a character data type. The type specifier for characters is char.

Once a character is stored in memory as a binary value, the binary value can be interpreted as a character or as an integer. Thus, when we define a variable for storing a character, we can define it as either a character variable to store the ASCII value or as an integer variable to store the integer equivalent value. However, it is important to note that the binary ASCII representation for a character digit is not equal to the binary representation for an integer digit. From Table 2.3, we see that the ASCII binary representation for the character digit 3 is 0110011, which is equivalent to the binary representation of the integer value 51. Thus, performing a computation with the character representation of a digit does not yield the same result as performing the computation with the integer representation of the digit. The following program illustrates the use of character data. The details of the program are discussed later in the chapter.

![](img/02c4582f051c5b51776411c92b079035_55_0.png)

## Table 2.3 Examples of ASCII Codes

| Character | ASCII Code | Integer Equivalent |
|---|---|---|
| newline, \n | 0001010 | 10 |
| % | 0100101 | 37 |
| 3 | 0110011 | 51 |
| A | 1000001 | 65 |
| a | 1100001 | 97 |
| b | 1100010 | 98 |
| c | 1100011 | 99 |

```
/*
 * Program chapter2_1
 *
 *
 * This program prints two values
 * as characters and integers.
 */
#include <stdio.h>

int main(void)
{
    /* Declare and initialize variables. */
    char ch='a';
    int i=97;

    /* Print both values as characters. */
    printf("value of ch: %c; value of i: %c \n",ch,i);

    /* Print both values as integers. */
    printf("value of ch: %i; value of i: %i \n",ch,i);

    /* Exit program. */
    return 0;
}
/*--------------------------------------------------*/
```

The output from this program is

```
value of ch: a; value of i: a
value of ch: 97; value of i: 97
```

## Symbolic Constants

A symbolic constant is defined with a preprocessor directive that assigns an identifier to the constant. The directive can appear anywhere in a C program; the compiler will replace each occurrence of the directive identifier with the constant value in all statements that follow the directive. Engineering constants such as $\pi$ or g (the acceleration due to gravity) are good candidates for symbolic constants. For example, consider the following preprocessing directive to assign the value 3.141593 to the variable PI.

![](img/02c4582f051c5b51776411c92b079035_56_0.png)

```
#define PI 3.141593
```

Statements that need to use the value of $\pi$ would then use the symbolic constant identifier PI instead of 3.141593, as illustrated in the following statement which computes the area of a circle:

```
area = PI*radius*radius;
```

![](img/02c4582f051c5b51776411c92b079035_56_1.png)

Symbolic constants are usually defined with uppercase identifiers (as in PI instead of pi) to indicate that they are symbolic constants, and, of course, the identifiers should be selected so that they are easy to remember. Finally, only one symbolic constant can be defined in a directive; if several symbolic constants are desired, separate directives are required. Note that preprocessor directives, which include the `#define` statement, do not end with a semicolon.

![](img/02c4582f051c5b51776411c92b079035_56_2.png)

In the next section, we discuss C statements that allow us to assign values to variables. These assignment statements could be used to assign constant values to variables, but we will see later that there are often some special advantages to using symbolic constants.
