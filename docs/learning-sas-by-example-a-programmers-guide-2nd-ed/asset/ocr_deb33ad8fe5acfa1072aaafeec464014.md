# 264 Learning SAS as Example: A Programmer's Guide, Second Edition

You now have your descriptive statistics for males and females separately, as shown next:

Figure 16.3: Output from Program 16.3

# Adding a BY Statement to PROC MEANS

Gender=Female

| Variable | N | N | Miss | Mean | Median | Minimum | Maximum |
| --- | --- | --- | --- | --- | --- | --- | --- |
| RBC | 409 | | 31 | 5.5 | 5.6 | 1.7 | 8.8 |
| WBC | 403 | | 37 | 7112.4 | 7150.0 | 4620.0 | 10260.0 |

Gender=Male

| Variable | N | N | Miss | Mean | Median | Minimum | Maximum |
| --- | --- | --- | --- | --- | --- | --- | --- |
| RBC | 507 | | 53 | 5.5 | 5.5 | 2.3 | 8.4 |
| WBC | 505 | | 55 | 6987.5 | 6930.0 | 4070.0 | 10550.0 |

# 16.4 Using a CLASS Statement with PROC MEANS

PROC MEANS lets you use a CLASS statement in place of a BY statement. The CLASS statement performs a similar function to the BY statement, with some significant differences. If you are using PROC MEANS to print a report and are not creating a summary output data set, the differences in the printed output between a BY and CLASS statement are basically cosmetic. The main difference, from a programmer's perspective, is that you do not have to sort your data set before using a CLASS statement. To demonstrate this, run Program 16.3, substituting the CLASS statement for the BY statement, as follows:

# Program 16.4: Using a CLASS Statement with PROC MEANS

```
title "Using a CLASS Statement with PROC MEANS";
proc means data=Learn.Blood n miss mean median
    min max maxdec=1;
  class Gender;
  var RBC WBC;
run;
```

Notice that you are using the permanent SAS data set (that may not be sorted) instead of the temporary sorted data set used in Program 16.3. There are some minor differences in the appearance of the printed output, as shown here: