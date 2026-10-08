| | Valid | Reason |
| :--- | :--- | :--- |
| 10,000 | No | Comma not allowed |
| –200.0 | No | A real value not allowed in integer |
| Rs 2569 | No | Alphabets are not allowed |
| 0xBN | No | N is not a valid letter in hexadecimal number system |
| 0X2,3 | No | Comma is not allowed |
| O58 | No | 8 is not part of octal number system |
| 055.8 | No | Period not allowed |

# Real Constant

Real constant refers to decimal numbers that have fractional part. Examples of real constant are 99.657, –53.42, and so on. Real constant can also be represented by using scientific notation. In this form, a number is represented by using a *mantissa* and an exponent. For example, the value 53.42 can be represented as $0.5342 \mathrm{e} 2$ or $0.5342 \mathrm{E} 2$, where $0.5342$ is known as mantissa and 2 as exponent. A list of some valid and invalid real constants as per C language rules is listed in Table 7:

| | Valid | Reason |
| :--- | :--- | :--- |
| 25.50 | Yes | Valid decimal fractional number. |
| 75 | Yes | Valid decimal number. Automatically converted to 75.00. |
| –55.9999 | Yes | Valid negative decimal number. |
| –25e5 | Yes | Valid scientific value. |
| 50.75E-2 | Yes | Valid scientific value. |
| 4,999.00 | No | Comma not allowed. |
| $5555 | No | Special character not allowed. |
| –7.5e2.0 | No | Exponent should be integer. |
| 989 E -2 | No | Blank spaces not allowed. |
| 5e8E-2 | No | Use of multiple E not allowed. |

# Character constant

Character constants, as the name suggests, consist of single or set of characters. There are two types of character constant in C language: single-character constant and string constant.

# Single-Character Constant

A single-character constant is represented by using single character enclosed within single quotes. Each character constant in C is associated with a numeric value known as the American Standard Code for Information Interchange (ASCII) value. Appendix II in the