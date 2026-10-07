DEFINE statement for HR adds a label (placed in quotes) and a column width. Look at the output here to see the effect of these two DEFINE statements:

Figure 15.5: Output from Program 15.5

| Heart Rate | Weight |
| 78 | 120 |
| 58 | 166 |
| 68 | 210 |
| 88 | 288 |
| 54 | 180 |
| 60 | 199 |

You now see a detailed listing of every observation rather than a single summary statistic.

# 15.5 Producing a Summary Report

For this, you want to use the mean heart rate and mean weight for each clinic in the Medical data set. To do this, you need to use the GROUP usage for the variable Clinic. In addition, you need to specify MEAN as the statistic for heart rate and weight. Program 15.6 does the:

Program 15.6: Specifying a GROUP Usage to Create a Summary Report

```
title "Demonstrating a GROUP Usage";nproc report data=learn.medical;
column Clinic HR;
define Clinic / group width=11;
define HR / analysis mean "Average Heart Rate" width=12
format=5;
define Weight / analysis mean "Average Weight" width=12
format=6;
```

run;

The MEAN statistic, along with a format, is specified for each of the numeric variables. The keyword ANALYSIS is optional because this is the default usage for numeric variables. You may place these options (label, width, format, and so on) in any order you like. The report is shown next: