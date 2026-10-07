# 318 Learning SAS by Example: A Programmer’s Guide, Second Edition

Figure 18.24: Output from Program 18.22

| | B | All |
|---|---|---|
| | X | Y | Z |
| | N | N | N |
| A | | | |
| X | 1 | 1 | 2 No Data 4 |
| Y | No Data No Data No Data | 1 1 |
| Z | No Data No Data No Data | 1 1 |
| All | 1 | 1 | 2 6 |

We hope that this introduction to PROC TABULATE gives you the courage to give this useful and powerful procedure to try. Author was TABULATE-phobic for a long time until forced to use the procedure for a project that requires nice-looking summary tables. Now, it is a convert and tries to get others to use this procedure more.

# 18.14 Problems

Solutions to odd-numbered problems are located at the back of this book. Solutions to all problems are available to professors. If you are a professional, visit the book’s companion website at support.sas.com/coded for information about how to obtain the solutions to all problems.

All the problems, except Problem 10, use the SAS data set College.

Note: Data set College has permanent formats for Gender, SchoolSize, and Scholarship. Make this format catalog available to SAS (see Chapter 5), run the PROC FORMAT statements here, or use the system option NOFORMATTER (no format error) that allows you to access SAS data sets that have permanent-defined formats without causing any error.

```
proc format;
value$Yesno '1' = 'Yes'
      '0' = 'No'
      '' = 'Not Given';
value$Size 'S' = 'Small'
      'M' = 'Medium'
      'L' = 'Large'
      '' = 'Missing';
value$Gender 'F' = 'Female'
      'M' = 'Male'
      '' = 'Not Given';
```

run;