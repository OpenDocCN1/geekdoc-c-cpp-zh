# Chapter 24: Working with Multiple Observations per Subject

The NPRINT option is included because you want PROC FREQ to create a data set and you do not need printed output. In this program, you name the data set Counts. PROC FREQ uses the variable names Count and Percent for the variables representing the frequencies and percentages for each value of the variable listed in the TABLES statement. This is clear if you look at the listing of data counts created by Program 24.3.

Figure 24.4: Listing of Data Set Counts

| ID | COUNT | PERCENT |
|---|---|--|
| 101 | 2 | 16.666 |
| 255 | 4 | 33.3333 |
| 303 | 1 | 8.3333 |
| 409 | 3 | 25.0000 |
| 712 | 2 | 16.666 |

You can use the RENAME= and DROP= KEEP= options to control what variables are in this data set and what they are called. For example, the next program renames Counts to N. Visits and drops the Percent variable. In addition, a MERGE statement adds the variable N_Visits to each observation in the original Clinic data set. Here is the program:

# Program 24.4: Using the RENAME= and DROP= Data Set Options to Control the Output Data Set

```
proc freq data=Clinic noprint;
rename=(count = N_Visits)
tables ID /outCounts (rename=droppercent);
run;
data Clinic;
merge Learn.Clinic Counts;
by ID;
run;
```

The RENAME= data set option renames the variable Count (the name chosen by SAS) to N_ Visits. The DROP= data set option tells SAS that you don't want the variable Percent in the new data set. You don't need to sort data set Counts because it will be in ID order. The default ordering for PROC FREQ is to order values by their internal (unformatted) values. Data set Clinic is already in ID order. Here is the result: