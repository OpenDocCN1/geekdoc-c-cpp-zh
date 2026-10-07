```
DATA NEW;SET TRANSPOSED;
RENAME INFO1=T1 INFO2=T2 INFO3=T3 INFO4=T4 INFO5=GENDER;
RUN;
PROC PRINT DATA=NEW;
RUN;

Submit this code and verify that it provides better names for the data set.
```

Another possibility when transposing data is to use an available label to name new variables. Consider the following code (DTRANPOSE1A.SAS):

```
DATA SUBJECTS;
INPUT LAB $ SUB1 $ SUB2 $ SUB3 $ SUB4 $;
DATALINES;
BASELINE 12 21 13 14
TIME1 13 21 12 14
TIME2 15 31 23 23
TIME3 15 33 21 32
GENDER M F F M

PROC TRANSPOSE DATA=SUBJECTS OUT=TRANSPOSED;
ID LAB;
VAR SUB1 SUB2 SUB3 SUB4;
RUN;
PROC PRINT DATA=TRANSPOSED;
RUN;
```

In this version of the program, there is a variable called LAB that provides a label for columns. The ID statement in PROC TRANSPOSE allows you to specify LAB for the new variables.

# HANDS-ON EXAMPLE

+   1. Open the file DTRANPOSE1A.SAS. Submit the code and observe the output given in Table 6.3.

PROC TRANSPOSE DATA=SUBJECTS OUT=TRANSPOSED;
ID LAB;
VAR SUB1 SUB2 SUB3 SUB4;
RUN;

Because of the ID statement in PROC TRANSPOSE, the values for ID become the column names.
2. Change the values in the data set from BASELINE, TIME1, and so on to READ1 through READ4. Leave GENDER as is. Resubmit the code and note the changed variable names.