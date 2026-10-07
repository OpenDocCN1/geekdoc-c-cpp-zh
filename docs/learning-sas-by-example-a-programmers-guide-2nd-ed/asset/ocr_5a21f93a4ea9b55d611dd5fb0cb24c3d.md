This request nests AgeGroup and ALL within each value of Gender and ALL. The means of RBC, WBC,
and Chol are displayed as columns of the table, like this:

Figure 18.10: Output from Program 18.9

# Combining CLASS and Analysis Variables

| | RBC | WBC | Cholesterol |
|---|---|---|---||
| Gender Age Group | Mean | Mean | Mean |
| Female Old | | 5.48 | 7,105.98 | 195.88 |
| | Young | | 5.53 | 7,121.36 | 212.27 |
| | All | | 5.50 | 7,112.43 | 202.50 |
| Male Age Group | | | |
| Old | | 5.44 | 6,939.35 | 199.12 |
| | Young | | 5.52 | 7,061.66 | 203.08 |
| | All | | 5.47 | 6,987.54 | 200.60 |
| All Age Group | | | |
| Old | | 5.46 | 7,011.56 | 197.73 |
| | Young | | 5.52 | 7,088.09 | 207.29 |
| | All | | 5.48 | 7,042.97 | 201.44 |

# 18.7 Customizing Your Table

PROC TABULATE allows you to customize your table in several ways. You can associate a format with
the table or rename any of the keywords, such as ALL or MEAN.

If you look back at the output produced by Program 18.7, you see that the default format is useful for
values of RBC but not for values of WBC (where you would rather not see any decimal values). The
program follows a different format with each of these two variables:

Program 18.10: Associating a Different Format with Each Variable in the Table

```
title "Specifying Form"
proc table data=Learn.Blood;
var RBC WBC;
table RBC*mean=f=7.2 WBC*mean=f=comma7;
run;
```

Here you see another use of the asterisk. It is used to associate a format with a specific value. You can
th of the formatting being nested within the statistic.