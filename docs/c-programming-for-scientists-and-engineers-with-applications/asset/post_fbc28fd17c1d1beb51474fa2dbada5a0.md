
Notice that 5000 is the memory location (address) of the variable var1 and 6000 is the memory location (address) of the pointer variable ptrvar1. Executing the assignment places the address of var1 in the storage of ptrvar1.

Now the value for the variable var1 may be accessed by the variable name var1 or through the pointer variable ptrvar1. To access the value of var1 through the pointer ptrvar1 a dereference operator (*) must be used. The following code shows the use of the dereference operator.

Before

address
| var1 | address |
|---|---|
| 5000 | 460.58 |

*ptrvar1 = 723.14;

After

address
| var1 | address |
|---|---|
| 5000 | 723.14 |

```
ptrvar1 = &var1;
*ptrvar1 = 723.14;
is equivalent to
var1 = 723.14;
```

Similarly the assignment statement *ptrvar1 = *ptrvar1 + 200; *ptrvar1 on the right of the assignment accesses the value of 723.14 from the storage of the variable var1 and then adds 200 and stores the altered value 923.14 in var1 using the pointer dereference.

Before

address
| var1 | address |
|---|---|
| 5000 | 723.14 |

*ptrvar1 = 200 + *ptrvar1;

- 2. Answer the following questions:
a. Declare the following variables as integer variables.
- iter, counter
- i, j, k
- max, min, ival, imax, jmax
b. Declare and initialize the following variables to the values specified.
- maxcount to 50, ic to 20, kvalue to 100
c. Declare the following variables as floating-point variables.
- balance, energy, power, voltage, current, acidity, phvalue
d. Declare the following variables as double-precision variables.
- atomic-number, refractive-index, specific-gravity, density
e. Declare the following variables as character variables.
- code, basic colors, student_status, depth_code.

f. Declare and define the following constants, giving them the obvious values.
- three, plus, e, gravity

- 3. Answer the following questions
a. In C the built-in data types are \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
and \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_
b. In C the derived data types are \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\, and \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_.

## 2.3 Arithmetic Operations and Expressions

Engineering and scientific computing involves arithmetic operations and arithmetic expressions. Arithmetic operations can be performed on numeric data of type int, float, and double, which have the usual arithmetic operations built into the language. Millions of arithmetic operations are performed every day in engineering and scientific calculations. Computers are designed to perform them very quickly.

### 2.3.1 Arithmetic Operators and Operations

The basic arithmetic operations are expressed in C using the following symbols:

- addition +
- subtraction -
- multiplication *
- division /
- nremainder %

Each of these has multiple meanings depending on the declared types of the operands.

Exponentiation is performed in C by using the function pow(double, double), from the math library. The addition and subtraction symbols can be used with either one operand a unary plus (e.g., +245), a unary minus (e.g., -12), or two operands (to indicate addition or subtraction). Unary operators should be separated by parentheses so that two operators do not immediately follow each other. The following examples show the use of the operators.

Unary plus:
Addition operation:

| Expression | Value |
|---|---|
| +(+15) | 15 |
| 8 + 5 | 13 |
| -8 + 15 | 7 |
| 18 + (-25) | -7 |
| -15 + (-18) | -33 |
| 18.54 + 3.21 | 21.75 |
| -0.124 + 1.23 | 1.106 |

Unary minus:

| -(-10) | 10 |
| -23.321 | -23.321 |

Subtraction operation:

| 12 - 8 | 4 |
| -16 - 7 | -23 |
| 8 - (-6) | 14 |
| -5.67 - 2.43 | -8.10 |
| 9.98 - 6.33 | 3.65 |

Multiplication operation:

| 8 * 4 | 32 |
| 6 * (-4) | -24 |
| 2.5 * 3 | 7.5 |

Division operation:

| 16/2 | 8 |
| 20/(-4) | -5 |
| -5/5 | -10 |
| 14/5 | 2.8 |
| 6.6/2 | 3.3 |

> **Programming warning:** Division of an integer by an integer produces an integer. When both operands are integers, the result of division is an integer. This may lead to undesirable results involving integer division where the fractional part is not rounded but is truncated. If a division expression has two operands as integers, to keep the fractional part you must cast one or both the integers to either float or double as shown in the following examples. (float)7/4 or (float)7/(float)4 or 7.0/4.0 will give the result 1.75. Preceding the number by a data type converts the number to real by adding a decimal point.

Remainder Operation | Value | Mathematics |
|---|---|---|
| 8 % 3 | 2 | 8 /3=2 |
| 16 % 2 | 0 | 16/2 = 0 |
| 15 % 4 | 3 | 15/4=3 R 3 |
| (-8) % 3 | -2 | -8 /3=-2 R -2 |

Notice that the remainder operation is restricted to the integer data type. R stands for remainder. This operator is also called a modulo operator and reads as “8 mod 3.”

Exponentiation Operation The pow function from the math library is used for exponentiation. The arguments must be of double. The general expression is as follows:

```
pow((double) a, (double) b)
```

| Expression | Operation | Value |
|---|---|---|
| 5² | pow((double) 5, (double) 2) | 25.0 |
| (-5)² | pow((double) -5, (double) 2) | 25.0 |
| 2⁵ | pow((double) 2, (double)(.5)) | 1.414 |
| 2⁻⁵ | pow((double) 2, (double)(-.5)) | 0.707 |

If the base a and the exponent b are declared as double precision variables, the pow function call is as follows:

```
double x, y;
pow(x, y);
```

Notice that the exponentiation operation is restricted to the double data type.

Table 2.3 Data type of mixed mode arithmetic
| | int | float | double |
|---|---|---|
| operand1 | int | float | double |
| float | float | double |
| double | double | double |

**Mode of Arithmetic Results** If the two operands of an arithmetic operation are of the int type the result is an int value. If the two operands are float the result is float. If the two operands are of the same type the result is the same data type as the operands. If the two operands are mixed (e.g., one operand is int and the other is float, the arithmetic is known as mixed-mode arithmetic*) and the result has the float data type. Table 2.3 shows the data type of the result when mixed-mode arithmetic is involved. The following examples show mixed-mode operations:

| Expression | Result |
|---|---|
| 16 + 2.0 | 18.0 |
| 15 - 12.5 | 2.5 |
| 15/3.5 | 4.285728 |
| 15.0/2 | 7.5 |

> **Programming Warning:** When doing mixed-mode arithmetic, be careful about the integer division operation. Make sure to cast one of the operands in such operation to data type float or double the decimal digits will be lost.

When arithmetic is performed using both integer and floating-point operands, the computer has to change the integer operand to a floating-point number before performing the arithmetic, for example

| 15 + 6.0 becomes | 15.0 + 6.0 with the result | 21.0 |
| 18.5 / 2 becomes | 18.5 / 2.0 with the result | 9.25 |
| 12.25 * 2 becomes | 12.25 * 2.0 with the result | 24.50 |

When a double-precision value is used in a mixed-mode operation with an integer or single-precision value, the integer or single-precision value is converted to double-precision before the operation is performed. The result is a double-precision value that has no more accuracy than the less accurate of the two operands.

### 2.3.2 Arithmetic Expressions

In engineering and scientific applications it is very common to use arithmetic expressions that include constants as well as variables. An expression can be used in a C program wherever a value of the same type can be used. The examples show arithmetic expressions and the results for the following variable declarations:

int a, b, c, d;
float x, y, z, w;

| Expression | Result |
|---|---|
| 5 + 6 * 8 / 2 | integer constant |
| 3.0 + 5 * 2.5 + 6.0 / 2 | floating-point constant |
| a + b * c - d / c | integer value |
| x - y * z + w / 2 | floating-point value |
| a * x - b / y + w / c | floating-point value |

### 2.3.3 Assignment Statement

The assignment statement is the fundamental statement in most programming languages, including C. In C the equal sign (=) is used in the assignment statement. This symbol does not have the same meaning that it does in algebraic expressions. The meaning of this symbol in C is like its meaning in mathematical formulas. It indicates that the value computed from the expression on the right of the equal sign is to be assigned to the variable on the left (or stored in the memory location allocated to the variable on the left side of the equal sign). The following examples show the assignment statement:

area = (3.141593 * d * d) / 4.0;

means calculate $\pi$ times the diameter squared and assign the result to area.

That is, the area of a circle.  $\pi$ has seven digits because values of data type float are stored with seven digits.
