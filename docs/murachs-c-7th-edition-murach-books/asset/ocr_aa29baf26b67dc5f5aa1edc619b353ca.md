# The syntax of the Format() method of the String class

```
Format(string, value1[, value2]...)
```

# The syntax of a format specification within the string argument

```
{N[, M][:formatString]}
```

# Explanation

| N | An integer that indicates the value to be formatted. |
| M | An integer that indicates the width of the formatted value. If M is negative, the value will be left-justified. If it's positive, it will be right-justified. |
| formatString | A string of formatting codes. |

# The syntax of a format string

```
positiveformat[;negativeformat[;zeroformat]]
```

# Standard numeric formatting codes

| C or c | Formats the number as currency with the specified number of decimal places. |
| D or d | Formats an integer with the specified number of digits. |
| E or e | Formats the number in scientific (exponential) notation with the specified number of decimal places. |
| F or f | Formats the number as a decimal with the specified number of decimal places. |
| G or g | Formats the number as a decimal or in scientific notation depending on which is more compact. |
| N or n | Formats the number with thousands separators and the specified number of decimal places. |
| P or p | Formats the number as a percent with the specified number of decimal places. |

# Custom numeric formatting codes

| 0 | Zero placeholder | , | Thousands separator |
| # | Digit placeholder | % | Percentage placeholder |
| . | Decimal point | ; | Section separator |

# Statements that format a single number

```
string balance1 = String.Format("{0:c}", 1234.56);    // $1,234.56
string balance2 = 
    String.Format("{0:$#,##0.00;($#,##0.00)}", -1234.56);    // ($1,234.56)
string balance3 = 
    String.Format("{0:$#,##0.00;($#,##0.00);Zero}", 0);    // Zero
string quantity = String.Format("{0:d3}", 43);    // 043
string payment = String.Format("{0:f2}", 432.8175);    // 432.82
```

# A statement that formats two numbers

```
string totalDue = 
    String.Format("Invoice total: {0:c}; Amount due: {1:c}.", 354.75, 20);
// Invoice total: $354.75; Amount due: $20.00.
```