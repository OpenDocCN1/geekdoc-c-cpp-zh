Age frequencies are now grouped into three categories and the Likert scale for Ques5 has only three categories.

# 17.6 Problems Grouping Values with PROC FREQ

A problem can occur when PROC FREQ uses formatted values to create groups. When you use the keyword OTHER as a range you create a format, all values that do not match a format are grouped together. PROC FREQ assigns all of them to the value of the variable with the lowest value.

As an example, you have a data set (Grouping) with the following values:

Figure 17.5: Data Values from Data Set Grouping

| Obs | X | Obs | X | Obs | X |
| 1 | 2 | 5 | 4 | 9 | 5 |
| 2 | 2 | 6 | 4 | 10 | 5 |
| 3 | 3 | 7 | 4 | 11 | 5 |
| 4 | 3 | 8 | missing | 12 | 6 |

You write the following program:

Program 17.5: Demonstrating a Problem in How PROC FREQ Groups Values

```
proc format;
value Two
low-3 = 'Group 1'
4-5 = 'Group 2'
other = 'Other values';
run;
ntitle "Grouping Values (First Try)";
proc freq data=Learn.Grouping;
tables X / nocopercent;
format X Two.;
run;
```

Looking at the values in data set Grouping, you would expect to see four values in Group 1 and six values in Group 2, value for Other values and one missing value. Here is what you get:

Figure 17.6: Output from Program 17.5

| X | Frequency |
| Group 1 | 4 |
| Group 2 | 6 |
| Frequency Missing = 2 |