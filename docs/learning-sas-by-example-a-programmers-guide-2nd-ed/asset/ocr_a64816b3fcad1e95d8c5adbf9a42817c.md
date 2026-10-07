Let's use some of these options to customize the output. You will compute the number of missing and nonmissing values, the mean, median, minimum, and maximum for the variables RBC (red blood cells) and WBC (white blood cells) in the Blood data set. Finally, you will report all statistics to the nearest 10th. Here is the program:

# Program 16.2: Adding a VAR Statement and Requesting Statistics with PROC MEANS

```
title "Selected Statistics Using PROC MEANS";nproc means data=Learn.Blood n nmiss mean median
    min max maxdec=1;
var RBC;
run;
```

The output follows:

Figure 16.2: Output from Program 16.2

| Variable | N | Miss | Mean | Median | Minimum | Maximum |
|---|---|---|---|---|---||}{
| RBC | 916 | 84 | 5.5 | 5.5 | 1.7 | 8.8 |
| WBC | 908 | 92 | 7043.0 | 7040.0 | 4070.0 | 10550.0 |

You now have the statistics you requested on the variables listed in the VAR list. Notice that all the statistics are reported to one decimal place, due to the MAXDEC=1 option. (Unfortunately, the number of decimal places you choose is applied to all variables. If you need more control over the number of printed decimal places for each variable, you can use PROC TABULATE.) Values for N and NMISS are always integers.

# 16.3 Adding a BY Statement to PROC MEANS

If you want to see descriptive statistics for each level of another variable, you can include a BY statement, listing one or more BY variables. Remember that have to sort your data set first by the same variable or variables you list in the BY statement. Here are the same statistics displayed by Figure 16.2, broken down by gender:

# Program 16.3: Adding a BY Statement to PROC MEANS

```
proc sort data=Learn.Blood out=Blood;
    by Gender;
run;
ntitle "Adding a BY Statement to PROC MEANS";nproc means data=Blood n nmiss mean median
    min max maxdec=1;
    by Gender;
    var RBC;
run;
```