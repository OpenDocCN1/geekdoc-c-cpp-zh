# 254 Learning SAS by Example: A Programmer's Guide, Second Edition

As before, you include the variable you are computing in the COLUMN statement. The COMPUTE statement now includes the keyword CHARACTER to tell SAS that Rate is a character variable. The option LENGTH=6 defines the storage length for this variable.

Next, the logical statements to compute Rate are sandwiched between the COMPUTE and ENDCOMP statements. Here is the output:

Figure 15:18: Output from Program 15.18

| Patient Number | Heart Rate | Weight | Rate |
|---|---|---||}{
| 001 | 78 | 120 | Fast |
| 003 | 58 | 166 | Normal |
| 002 | 68 | 210 | Normal |
| 004 | 88 | 288 | Fast |
| 007 | 54 | 180 | Slow |
| 050 | 60 | 199 | Normal |

The new variable (Rate) is now included in the report.

# 15.16 Creating an ACROSS Variable with PROC REPORT

Besides creating column reports, PROC REPORT can also create a tabular style report with each unique value of a variable forming a new column in your report.

This is accomplished by using an ACROSS usage for your variable. In the example that follows, each type of bicycle (hybrid, mountain, and road) in the Bicycle data set is used to create a separate column in the report:

Program 15.19: Demonstrating an ACROSS Usage in PROC REPORT

```
***Demonstrating an Across Usage;
title "Demonstrating an ACROSS Usage"
proc report data=Learn.Bicycles;
  column Model,Units Country;
  define Country / group widths=14;
  define Model / across "Model";
  define Units / sum "# of Units" width=14
  format=comma8.;
run;
```

Besiding defining Model as an Across variable, you need to tell the procedure what value you want to display for each row of the table. Notice Model, Units terms in the COLUMN statement. This is an instruction to PROC REPORT to report the number of units within each category of Model. The listing here should help clarify how this works: