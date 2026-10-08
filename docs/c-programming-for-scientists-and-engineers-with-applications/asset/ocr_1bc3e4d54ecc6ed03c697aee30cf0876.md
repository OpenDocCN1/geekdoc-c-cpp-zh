# 2.3 Arithmetic Operations and Expressions

Table 2.3 Data type of mixed mode arithmetic
| | int | float | double |
|---|---|---|---||
| operand1 | int | float | double |
| float | float | float | double |
| double | double | double | double |

**Mode of Arithmetic Results** If the two operands of an arithmetic operation are of the int data type the result is an int value. If the two operands are float the result is float. If the two operands are of the same type the result is the same data type as the operands. If the two operands are mixed (e.g., one operand is int and the other is float, the arithmetic is known as *mixed-mode arithmetic*) and the result has the float data type. Table 2.3 shows the data type of the result when mixed-mode arithmetic is involved. The following examples show mixed-mode operations:

| Expression Result |
| 16 + 2.0 | 18.0 |
| 15 - 12.5 | 2.5 |
| 15/3.5 | 4.285728 |
| 15.0/2 | 7.5 |

> **Programming Warning:** When doing mixed-mode arithmetic, be careful about the integer division operation. Make sure to cast one of the operands in such operation to data type float or double the decimal digits will be lost.

When arithmetic is performed using both integer and floating-point operands, the computer has to change the integer operand to a floating-point number before performing the arithmetic, for example

| 15 + 6.0 becomes | 15.0 + 6.0 with the result | 21.0 |
| 18.5 / 2 becomes | 18.5 / 2.0 with the result | 9.25 |
| 12.25 * 2 becomes | 12.25 * 2.0 with the result | 24.50 |