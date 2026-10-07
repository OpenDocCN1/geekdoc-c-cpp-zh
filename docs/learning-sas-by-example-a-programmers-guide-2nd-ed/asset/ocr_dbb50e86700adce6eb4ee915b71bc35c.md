# 23.4 Converting a Data Set with One Observation per Subject to a Data Set with Several Observations per Subject: Using PROC TRANSPOSE

PROC TRANSPOSE can also be used to restructure SAS data sets. Sometimes, PROC TRANSPOSE provides a quick and simple solution—sometimes the PROC TRANSPOSE solution can be quite complicated. In general, a data step solution gives you more control over the restructuring process. As you will see in this first PROC TRANSPOSE example, you need to add some data set options (see Program 23.4) to achieve the same results as the original data step solution.

The following program attempts to solve the same problem as Section 23.2. You start out with a program that restructures the OnePer data set, but does not completely solve the problem. Here is the code:

# Program 23.3: Using PROC TRANSPOSE to Convert a Data Set with One Observation per Subject (First Attempt)

```
***Note: data set already in Subject order;
proc transpose data=Learn.OnePer

  by Subj;
  out=ManyPer;
  var Dx1-Dx3;
run;
```

PROC TRANSPOSE takes an input data set and outputs a data set where the original rows become columns and the original columns become rows. This BY SUBJECT statement performs the operation for each value of Subject. The result is the data set listed next.

Figure 23.3: Listing of Data Set ManyPer (Transpose Method)

# Listing of Data Set ManyPer

| Subj | NAME | COL1 |
| --- | --- | --- |
| 001 | Dx1 | 450 |
| 001 | Dx2 | 430 |
| 001 | Dx3 | 410 |
| 002 | Dx1 | 250 |
| 002 | Dx2 | 240 |
| 002 | Dx3 | |
| 003 | Dx1 | 410 |
| 003 | Dx2 | 250 |
| 003 | Dx3 | 500 |
| 004 | Dx1 | 240 |
| 004 | Dx2 | |
| 004 | Dx3 | |