# CHAPTER 4: PREPARING DATA FOR ANALYSIS

All of the data manipulation statements discussed in this chapter appear in your program code within the DATA step, except for PROC FORMAT. That is, they appear after the DATA statement and before the first RUN or PROC statement. Thus, all of the results of the data manipulations performed by these statements become part of the active data set.

# 4.1 LABELING VARIABLES WITH EXPLANATORY NAMES

SAS labels are used to provide descriptive names for variables. Data sets often contain cryptic variable names such as ID, SDP, WT, and so on. For people familiar with the data set, these make perfect sense. However, if you want to produce output that is readable by others, creating explanatory labels for variables is good practice. In SAS, this can be achieved by using the LABEL statement. The LABEL statement uses the format:

```
LABEL VAR1 = 'Label for VAR1'
VAR2 = 'Label for VAR2';
```

You can use single or double quotation marks in the LABEL statement, but you must match the type within each definition statement. When SAS prints out information for VAR1, it also includes the label, making the output more readable. The following program (DLABEL.SAS) illustrates these of labels.

```
DATA MYDATA;
INFILE 'C:\SASDATA\BPDATA.DAT'; * READ DATA FROM FILE;
INPUT ID $1 SBP 2-4 DBP 5-7 GENDER $8 AGE 9-10 WT 11-13;
LABEL ID = 'Identification Number'
SBP = 'Systolic Blood Pressure'
DBP = 'Diastolic Blood Pressure'
AGE = 'Age on Jan 1, 2000'
WT = 'Weight';
```

```
PROC MEANS;
VAR SBP DBP AGE WT;
RUN;
```

Notice that the LABEL statement is placed within the DATA step. Also, there is only one semicolon (;) in the LABEL statement, at the very end.
The output listings in Tables 4.1 and 4.2 show how the LABEL statement adds information to the output. The first set of output shows PROC MEANS output without the LABEL statement. Notice that all variable names are listed just as they were created from the INPUT statement in the DATA statement.

The next set of output from PROC MEANS is the same data, and in this case, the LABEL statement, as shown in the aforementioned example, is used. In this case, more informative labels are included in the output.

Follow the next Hands-on Example to add label definitions for a data set within the DATA step.