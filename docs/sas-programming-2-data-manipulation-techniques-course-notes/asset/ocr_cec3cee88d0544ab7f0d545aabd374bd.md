# Input Styles

Column input, formatted input, list input, and named input are all styles of writing INPUT statement specifications.

| Style | Use for Reading |
| Column input | Standard data in fixed columns |
| Formatted input | Standard and nonstandard data in fixed columns |
| List input | Standard and nonstandard data separated by blanks or some other delimiter |
| Named input | Standard data that is preceded by the name of the variable and an equal sign (=) |

# Standard and Nonstandard Data (Review)

Standard data is data that SAS can read without any additional instruction.

+   - Character data is always standard.
- Some numeric values are standard and some are not.

| Standard Numeric Data | Nonstandard Numeric Data |
| 58 | |
| 67.23 -23 | (23) $67.23 |
| 5.67E5 00.99 | 5,823 01/12/2010 |
| 1.2E-2 | 12May2009 |

The following are the only acceptable characters in a standard numeric field:

0 1 2 3 4 5 6 7 8 9 . E e e D d - +

Leading or trailing blanks are also acceptable.

E, e, and D represent exponential notation in a standard numeric field. An alternate way of writing 30000, for example, is 3E5.

Examples of nonstandard character data include preserving leading blanks in character values, hexadecimal characters, and values surrounded by matching quotation marks.