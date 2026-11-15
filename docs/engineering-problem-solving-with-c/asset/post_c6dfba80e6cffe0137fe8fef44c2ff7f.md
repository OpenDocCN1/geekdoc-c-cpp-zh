
## Practice 2.2 continued

In Problems 7 through 12, express the value in floating-point notation.

- 7. 1.03e-5
- 8. -1.05e5
- 9. -3.552e6
- 10. 6.67e-4
- 11. 9.0e-2
- 12. -2.2e-2

## Numeric Data Types

Numeric data types are used to specify the types of numbers that will be contained in objects. In C++, the built-in numeric types are either integers or floating-point values. The following diagram shows the built-in numeric data types and their specifiers that are discussed in the next few paragraphs:

![](img/0235a4ea835dc4575bd036e024a533b3_62_0.png)

type specifiers system dependent

The type specifiers for signed integers are short, int, and long, for short integer, integer, and long integer, respectively. The specific ranges of values are system dependent, which means that the ranges can vary from one system to another. In the last section of this chapter, we present a program that you can use to determine the ranges of the numeric data types on your system. On many systems, the short integer data type ranges from –32,768 to 32,767, and the integer and long integer type often represents values from –2,147,483,648 to 2,147,483,647. (The unusual limits such as 32,767 and 2,147,483,647 relate to conversions of binary values to decimal values.)

C++ also allows an unsigned qualifier to be added to integer specifiers. An unsigned integer can represent only positive values. Signed and unsigned integers can represent the same number of values, but the ranges are different. For example, if an unsigned short has the range of values from 0 to 65,535, then a short integer has the range of values from –32,768 to 32,767; both data types can represent a total of 65,536 values.

The type specifiers for floating-point values are float (single precision), double (double precision), and long double (extended precision). The following declaration statement from program chapter1_1 thus defines seven objects that all contain double-precision floating-point values:

```
double x1(1), y1(5), x2(4), y2(7),
side1, side2, distance;
```

A declaration statement defines an identifier and associates the identifier with a specific data type. An initial value may be specified for an identifier at the time it is declared. If an initial value is specified, that value defines the initial value of the identifier.

### Statement Box 2.1 Declarations

A declaration statement defines new identifiers and allocates memory. An initial value may be assigned to the memory location at the time the identifier is defined. Modifiers may also be specified. An initial value is required when using the const modifier.

### Syntax

```
[modifier] type specifier identifier [(initial value)];
[modifier] type specifier identifier [= initial value];
[modifier] type specifier identifier{(initial value)};
```

### Examples

```
double y1(0), x1;
int counter = 0, n(0);
const int MIN_SIZE=0;
bool error(false);
char comma(',');
```

There are multiple notations available for initializing objects. The notation double y1(0); is new to C++11 and is the recommended notation. The notation int counter = 0; is used in C as well as C++ and will be seen frequently in older codes. The notation int n(0); is also used frequently in existing C++ codes. We will use the new C++11 notation for most of our examples in this text.

The difference between the float, double, and long double types relates to the precision (or accuracy) and the range of the values represented. The precision and range are system dependent. Table 2.2 contains precision and range information for integers and floating-point values used by the Microsoft Visual C++ compiler. A program given in Section 2.10 allows you to obtain this information for your computer system. On most systems, a double data type stores about twice as many decimal digits of precision as are stored with a float data type. In addition, a double value will have a wider range of exponent values than a float value. The long double value may have more precision and a still wider exponent range, but this is again system dependent. A floating-point constant such as 2.3 is assumed to be a double constant. To specify a float constant or a long double constant, the letter (or suffix) F or L must be appended to the constant. Thus, 2.3F and 2.3L represent a float constant and a long double constant, respectively.

| Data Type | Limits |
|---|---|
| short | Maximum = 32,767 |
| int | Maximum = 2,147,483,647 |
| long | Maximum = 2,147,483,647 |
| float | 6 digits of precision<br>Maximum exponent = 38<br>Maximum value = 3.402823e + 38 |
| double | 15 digits of precision<br>Maximum exponent = 308<br>Maximum value = 1.797693e + 308 |
| long double | 15 digits of precision<br>Maximum exponent = 308<br>Maximum value = 1.797693e + 308 |

## Boolean Data Type

The boolean data type, named after the mathematician George Boole, can represent only two values: true and false. In C++, the value zero is interpreted as false and any nonzero value is considered to be true. There are two predefined boolean constants, true and false, that can also be used. Boolean objects can be defined using the type specifier bool. The following example illustrates the use of boolean objects and constants:

```
bool error(false), status(true);
cout << error << endl << status;
```

The output from this program is

```
0
1
```

Boolean objects are very useful in controlling the flow of a program and flagging error conditions.

## Character Data Type

Character data is easy to work with in C++, but to work with characters effectively, we need to understand more about their representation in the computer's memory. Recall that all information stored in a computer is represented internally as sequences of binary digits (0 and 1). Each character corresponds to a binary code value. In the discussions that follow, we assume that American Standard Code for Information Interchange (ASCII) code is used to represent characters. Table 2.3 contains a few characters, their binary form in ASCII, and the integer values that correspond to the binary values. The character 'a' is represented by the binary value 1100001, which is equivalent to the integer value of 97. A total of 128 characters can be represented in the ASCII code. A complete ASCII code table is given in Appendix B.

| Character | ASCII Code | Integer Equivalent |
|---|---|---|
| newline, \n | 0001010 | 10 |
| % | 0100101 | 37 |
| 3 | 0110011 | 51 |
| A | 1000001 | 65 |
| a | 1100001 | 97 |
| b | 1100010 | 98 |
| c | 1100011 | 99 |

![](img/0235a4ea835dc4575bd036e024a533b3_65_0.png)

A character constant is enclosed in single quotes, as in 'A', 'b', and '3'. The type specifier for character objects is char. Once a character is stored in memory as a binary value, the binary value can be interpreted as a character or as an integer, as illustrated in Table 2.3. It is important to note that the binary ASCII representation for a character digit is not equal to the binary representation for an integer digit.

From Table 2.3, we see that the ASCII binary representation for the character digit '3' is 0110011, which is equivalent to the binary representation of the integer value 51. Thus, performing a computation with the character representation of a digit does not yield the same result as performing the computation with the integer representation of the digit. The following program illustrates this feature of character data:

```
/*
* Program chapter2_1
* This program prints a char and an int
*/
#include<iostream> // Required for cout
using namespace std;

int main()
{
    // Declare and initialize objects.
    char ch('3');
    int i(3);

    // Print both values.
    cout << "value of ch: " << ch << " value of i: " << i << endl;

    // Assign character to integer
    i = ch;

    // Print both values.
    cout << "value of ch: " << ch << " value of i: " << i << endl;

    // Exit program
    return(0);
}
/*------------------------------------------------------------*/
