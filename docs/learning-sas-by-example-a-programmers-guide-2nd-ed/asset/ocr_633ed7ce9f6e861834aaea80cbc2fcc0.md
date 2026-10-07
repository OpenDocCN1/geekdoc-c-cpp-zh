52 Learning SAS by Example: A Programmer’s Guide, Second Edition

This code code generates the following output:

**Figure 4.10:** Output from Program 4.6

Listing of Test_Scores
| Obs | ID | Name | Score1 | Score2 | Score3 |
|---|---|---|---|---|--|
| 1 | 1 | Jan | 90 | 95 | 98 |
| 2 | 2 | Preston | 78 | 77 | 99 |
| 3 | 3 | Russell | 88 | 91 | 92 |

This listing displays all the variables and all the observations in the Test_Scores data set.

Program 4.6 is an example of a procedure that uses all the default actions. That is, you did not specify any details such as variables to print or other controllable aspects of this procedure. Chapter 14 describes how to add options and statements to PROC PRINT to customize your report.

# 4.8 Using a SAS Data Set as Input to a DATA STEP

Besides raw data files, SAS data sets can also be used as input to a DATA step. As an example, you might want to use the information in an SAS data set to compute new variables.

Consider the data set Test_Scores (stored in the C:\books\learning folder). This data set contains the variables ID, Name, and Score1–Score3 (three scores). You want to compute an average score for each subject in this data. Program 4.7 performs this task:

**Program 4.7:** Using Observations from a SAS Data Set as Input to a New SAS Data Set

```
libname Learn 'C:\books\learning';

Data New;
set Test_Scores;
AveScore = mean(of Score1-Score3);
run;

title "Listing of Data Set New";
proc print data=New;
var ID Score1-Score3 AveScore;
run;
```

The key to this program is the SET statement. You can think of a SET statement as an INPUT statement except you are reading observations from a SAS data set instead of lines from a raw data file. There is a difference, each time you read a line of data from a raw data file, the variables being read from the raw data file or created by assignment statements in the DATA step are initialized to a missing value during each iteration of the DATA step. Variables that are read from SAS data sets are not set to missing values during each iteration of the DATA step—they are said to be retained. In Program 4.7, the variables ID, Name, and Score1–Score3 are retained; this is not a concern to us here, but it can be used in advantage in more advanced programs.