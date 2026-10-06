# Strings

# 7.2.1 Number Formatting

The code part of a format specification for a value of numeric type may be a standard number formatting code, which has the form c or cy or cyyy, where c is a character and y is a digit. The following number formatting codes are predefined for integers (I) or floating-point numbers (F) or both (IF):

| Code | String Format | Precision Specification or yy | Type |
|---|---|---|--|
D o r | Decimal number (possibly padded with zeros) | Minimum number of digits | I |
| X o r | Hexadecimal (possibly padded with zeros) | Minimum number of digits | |
| G o g | General (default) | Max. number of significant digits | IF |
| N o r | Number with thousands separators | Number of fractional digits | IF |
| F o f | Fixed-point number | Number of fractional digits | F |
| R o r | Lossless value-string conversion | (none) | |
| E o e | Exponential notation | Number of fractional digits | IF |
| P o p | Percent (value multiplied by 100 %) | Number of fractional digits | IF |
| C o c | Currency amount | Number of fractional digits | IF |

The code part of a format specification for a value of numeric type may also be a custom formatting pattern, which may be a combination of one or more of the predefined custom formatting codes:

```
0 # . , # E0 e0 E+ E-0 e-0 ; 'string' "string"
```

See example 29 and the .Net Framework class documentation for details.

# 7.2.2 DateTime Formatting

The code part of a format specification for an object of DateTime may be one of the predefined standard DateTime formatting codes:

| Code Character | Format |
|---|--|
| F o r | Full date and time, with (F) or without (f) seconds |
| G o g | General date and time, with (G) or without (g) seconds |
| s | Sortable date and time in ISO8601 format |
| u | Universal local date and time |
| U | Universal local date and time: F converted to UTC |
| R and r | RFC1123 standard full date and time |
| D o r | Full date, long (D) or short (d) format |
| Y and y | Year and month |
| M and m | Month and date |
| T or t | Time, with (t) or without (t) seconds |

The code part of a format specification for an object of DateTime may also be a custom DateTime formatting pattern, which may be a combination of one or more of the predefined custom DateTime formatting codes. See the .Net Framework documentation for details.