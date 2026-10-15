# Display 8.16 Reading date, time, and currency data into SAS

```
data test;
  input @1 date MMDDYY10. @21 time TIME8. @31 money DOLLAR10.2;
  datalines;
01/01/1960      01:00:00  $100.22
09/29/2003      09:49:59  $12693.79
;
run;

ODS RTF file="C:\Users\baileraj.IT\Desktop\Display-8-16.rtf";
proc print data=test;
title "print of date and time w/o formatting - internal SAS representation";
var date time money;
run;

proc print data=test;
title "print of date and time w/ formatting";
var date time;
format date MMDDYY10. time TIME8. money DOLLAR10.2;
run;
ODS RTF CLOSE;
```

A comparison of printing this data with and without formats is shown in Display 8.17.

# Display 8.17 Output from PROC PRINT of data containing date, time, and currency

| proc print;
var date time money; | proc print;
var date time money;
format date MMDDYY10. time TIME8.
money DOLLAR10.2; |
|---|---|---|
| Obs | date | time | money | Obs | date | time | money |
| 1 | 0 | 3600 | 100.22 | 1 | 01/01/1960 | 1:00:00 | $100.22 |
| 2 | 15977 | 35399 | 12693.79 | 2 | 09/29/2003 | 9:49:59 | $12,693.79 |

# 8.3 Recoding and Transforming Variables in a DATA Step

The DATA step is the hub of a lot of action defining, redefining, and transforming variables for later analyses. Common transformation examples include a variance-stabilizing or linearizing transformation of a response variable, the definition of higher