# 4.2 Controlling when a Record Loads

# Line Pointer Controls

Partial SAS Log

NOTE: 48 records were read from the infile 'address.dat'.
The minimum record length was 18.
The maximum record length was 30.
NOTE: The data set WORK.CONTACTS has 12 observations and 3 variables.

![](bbox=[0.036, 0.066, 0.638, 0.396])

# Line Pointer Controls

```
proc print data=contacts noobs;
run;
```

Partial PROC PRINT Output

| FullName | Address2 | Phone |
| --- | --- | --- |
| Ms. Sue Farr | Macon, CA 31298 | 869-7008 |
| Dr. Kay B. Cox | Kern, CA 93280 | 483-3321 |
| Mr. Ron Mason | Miami, FL 33054 | 589-9030 |
| Ms. G. H. Ruth | Munger, MI 48747 | 754-3582 |

![](bbox=[0.036, 0.423, 0.638, 0.723])