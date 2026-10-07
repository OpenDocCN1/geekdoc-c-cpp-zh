# 306 Learning SAS by Example: A Programmer's Guide, Second Edition

# Program 18.8: Specifying More than One Descriptive Statistic with PROC TABULATE

```
title "Specifying More than One Statistic";nproc tabulate data=Learn.Blood format=comma9.2;
var RBC WBC;
table (RBC WBC) * (mean min max);
run;
```

Each statistic is now listed for each of the two variables, this:

# Figure 18.9: Output from Program 18.8

# Specifying More than One Statistic

| RBC | | WBC |
| Mean Min Max | Min Max |
| 5.48 1.71 8.75 | 4.07.00 10.5500 |

This program uses the PROC TABULATE option FORMAT=COMMA9.2 to improve the readability of the output. Now you have the mean, minimum, and maximum value for RBC and WBC counts, each displayed with a 9.2 numeric format.

# 18.6 Combining CLASS and Analysis Variables in a Table

What if you want to see the mean value for RBC and WBC broken down by one or more of the CLASS variables (such as Gender or BloodType). You can combine frequencies and descriptive statistics in a single table. Here is where some people complain that PROC TABULATE is very difficult to use, Actually, the problem is more likely that the user did not decide what the table should look like before starting to write the TABULATE statements. It also takes some practice to arrange a table so that columns are not split between pages (making it very hard to read).

The next program is a request for the mean RBC, WBC, and Chol (cholesterol), broken down by Gender and AgeGroup.

# Program 18.9: Combining CLASS and Analysis Variables in the Table

```
title "Combining CLASS and Analysis Variables";nproc tabulate data=Learn.Blood format=comma1.2;
class Gender AgeGroup;
var RBC WBC Chol;
table (Gender ALL) * (AgeGroup All);
(RBC WBC Chol) *mean;
run;
```