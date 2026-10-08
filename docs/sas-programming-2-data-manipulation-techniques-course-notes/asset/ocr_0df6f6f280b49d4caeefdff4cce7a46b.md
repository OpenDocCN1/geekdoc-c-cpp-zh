# Automatic Character-to-Numeric Conversion

```
proc print data=hrdata noobs;
run;
```

| PROC PRINT Output |
| EmpID |
| 11036 11048 11052 |

The automatic conversion worked great for ID. Now see what happens with GrossPay.

# Automatic Character-to-Numeric Conversion

What happens when the character values of GrossPay are used in an arithmetic expression?

```
data hrdata;
  keep GrossPay Bonus;
  set orion.convert;
  Bonus=GrossPay * .10;
run;
```

orion.convert

| ID | GrossPay | Code | Mobile | Hired |
| $5 | $6 | $8 | $10 |
| 36 | 52,000 | 303 | 393-0956 | 04/13/2008 |
| 48 | 32,000 | 919 | 770-8292 | 08/25/2010 |
| 52 | 49,000 | 301 | 449-5239 | 06/08/2009 |