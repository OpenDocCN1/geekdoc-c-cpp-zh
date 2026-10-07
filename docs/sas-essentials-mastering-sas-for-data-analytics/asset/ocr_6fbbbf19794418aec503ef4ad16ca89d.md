# TABLE B.3 Arithmetic and Trigonometric Functions

| Function | Description |
|---|---|
| ARCOS (x) | Returns the value of arcosine |
| ARSIN (x) | Returns the value of arcsine |
| ATAN (x) | Returns the value of arctangent |
| COS (x) | Returns the value of cosine |
| COSH (x) | Returns the value of hyperbolic cosine |
| SIN (x) | Returns the value of sine |
| SINH (x) | Returns the value of hyperbolic sine |
| TAN (x) | Returns the value of tangent |
| TANH (x) | Returns the value of hyperbolic tangent |

# B.3 TRIGONOMETRIC FUNCTIONS

Each of these functions returns the specified trigonometric value for the value of the argument (in radians) entered into the function. For example,

```
Y=COS (3.14)
```

returns the value -1.000 (Table B.3).

# B.4 DATE AND TIME FUNCTIONS

SAS date and time values are stored as integers and indicate the number of days since 1/1/1960. A positive number indicates a date after 1/1/1960, and a negative number indicates a date before 1/1/1960. Date values that contain both date and time are stored in SAS as the number of seconds since midnight on 1/1/1960. Dates are typically displayed using a SAS date format as MMDDYYY10., which displays a date on 03/09/2016.

For these functions, a SAS date is a variable designated as a date value. Here are two examples of how values can be designated as dates:

+   - Assign a value to a fixed date. A d at the end tells SAS to interpret this quoted string as a date. For example (note that case does not matter either for the month abbreviation or for the "d")

```
BDATE = '12DEC1994d';
BEGINDATE ='11jan2011D';
EXAMDATE = '13-APR-2014d;
```

+   - Read a date as a date in an INPUT statement. For example,

```
INPUT BDATE MMDDYY10.;
```

In the following examples, a "date" is a SAS value that contains only a date, and a "datetime" value contains both date and time values.

When using date functions, beware of the "Y2K" problem. Any two-digit year lower than 20 is interpreted as being in the twenty-first century (e.g., the two-digit