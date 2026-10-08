# Explicit Character-to-Numeric Conversion

```
proc print data=hrdata noobs;
var EmpID GrossPay Bonus HireDate;
  format HireDate mmddyy10;
run;
```

PROC PRINT Output

| EmpID | Pay | Bonus | HireDate |
|---|---|---|---|
| 11038 | 52,000 | 5200 | 04/13/2008 |
| 11048 | 32,000 | 3200 | 08/25/2010 |
| 11052 | 49,000 | 4900 | 06/08/2009 |

What data type is GrossPay?

# Converting a Variable to Another Data Type

```
proc contents data=hrdata;
run;
```

Partial PROC CONTENTS Output Alphabetic List of Variables and Attributes

| | Variable | Type | Len |
|---|---|---|---|
| 3 | Bonus | Num | 8 |
| 2 | EmpID | Num | 8 |
| 1 | GrossPay | Char | 6 |
| 4 | HireDate | Num | 8 |

How can you convert GrossPay to a numeric variable with the same name?