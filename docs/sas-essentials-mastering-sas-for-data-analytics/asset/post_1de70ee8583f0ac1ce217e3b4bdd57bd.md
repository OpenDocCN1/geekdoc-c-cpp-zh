
# USING PROC SORT

```
1 1.5
1 1.8
PROC SORT DATA=MYDATA OUT=S1; BY RECTIME;
Title 'Sorting Example - Ascending';
PROC PRINT DATA=S1;
RUN;
```

Note that this program sorts the data and stores the results in a SAS data file named S1. Submit the code and observe the sorted output.

2. Write second PROC SORT and PROC PRINT statements to sort MYDATA descending and save the results in S2 by using the code

```
PROC SORT DATA=MYDATA OUT=S2; BY DESCENDING RECTIME;
```

Submit the revised program. Notice that the two PROC routines produce two different results, the data set S1 sorted ascending and data S2 sorted descending as shown in Table 4.10.

# TABLE 4.10 SAS Output Sorting Ascending and Descending Sorting Example - Ascending Sorting Example - Descending

| Obs | GROUP | RECTIME | Obs | GROUP | RECTIME |
|---|---|---|---|---|---|
| 1 | 2 | 1.5 | 1 | 2 | 4.2 |
| 2 | 1 | 1.8 | 2 | 2 | 3.8 |
| 3 | 1 | 2.1 | 3 | 2 | 3.6 |
| 4 | 1 | 2.8 | 4 | 1 | 3.1 |
| 5 | 2 | 3.1 | 5 | 1 | 2.8 |
| 6 | 2 | 3.6 | 6 | 1 | 2.1 |
| 7 | 1 | 4.2 | 7 | 1 | 1.8 |

Other handles in PROC SORT DROP, KEEP, and RENAME. These are illustrated in the following example.

# HANDS-ON EXAMPLE

Suppose you are sorting a data set for the purpose of merging it (which is discussed in the following section) and you need to change the variable name ID to CASE.

1. Open the program file DSORT2.SAS.

```
PROC SORT DATA="C:\SASDATA\SOMEDATA"
OUT=ANALYSIS;
(KEEP=ID AGE GENDER RENAME=( ID=SUBJECT AGE=DXAGE) );
BY ID;
RUN;
PROC PRINT DATA=ANALYSIS;RUN;
```

(continued)

# CHAPTER 4: PREPARING DATA FOR ANALYSIS

(continued)

Notice that there is a set of parentheses following the OUT= statement. Within those parentheses is a KEEP= statement that specifies variables to keep in the output file ANALYSIS. Inside these parentheses is another statement, RENAME with its own. Inside the RENAME= parentheses are two statements that rename an old variable with a name. The syntax of this RENAME statement is

```
RENAME = (oldname1=newname1 oldname2=newname2, etc...)
```

Therefore, this code renames two variables and saves four variables in the output. Submit this code and observe the (partial) results shown in Table 4.11.

However, note that the KEEP must be the original variable names, not the new names. Note that ID and AGE are kept, but in the new data set, they are named SUBJECT and GENDER.

- 2. The variable name GENDER out of the KEEP statement. Re-run the program and see that the results no longer include the GENDER column.

- 3. Re the GP to GROUP. Re-run the code and observe the changed results.

TABLE 4.11 SAS Output Showing Ascending and Descending
| Obs | SUBJECT | GP | DXAGE | GENDER |
|---|---|---|---|---|
| 1 | 101 | A | 12 | Female |
| 2 | 102 | A | 11 | Female |
| 3 | 104 | B | 12 | Female |
| 4 | 110 | A | 12 | Male |
| 5 | 103 | B | 0 | Male |

# 4.7 APPENDING AND MERGING DATA SETS

Other useful SAS data manipulation capabilities are appending and merging data sets.

- Adding adds records to an existing data set.
- Merging adds variables to a data set through the use of a key identifier that is present in both data sets (usually an identification code).

# 4.7.1 Appending Two Data Sets

Appending data sets combines records from two or more data sets (It is sometimes called a vertical merge.) For example, suppose that data sets are collected at two locations and you want to combine the data sets into one SAS data set for analysis. The data sets must have at least some of the same variables in common. Appending is accomplished by including multiple data set names in the SET statement. For example,

# APPENDING AND MERGING DATA SETS

DATA NEW; SET OLD1 OLD2;

creates the data set NEW, which consists of the records in the OLD1 data set, as well as the records from the OLD2 data set.

# HANDS-ON EXAMPLE

In this example, the program file will append one SAS data set to another, creating a larger data set.

- 1. Open the program file DAPPEND1.SAS.

```
DATA MYDATA;
DATA OLD1;
INPUT SUBJ $ AGE YRS_SMOKE;
DATALINES;
001 34 12
003 44 14
004 55 35
006 21 3
;
DATA OLD2;
INPUT SUBJ $ AGE YRS_SMOKE;
DATALINES;
011 33 11
012 25 19
023 65 45
032 71 55
;
RUN;
```

This program creates two data sets, one named OLD1 and the other named OLD2. It does not create any output. Run the program and verify by looking at the contents of the Log window that the data sets have been created. Observe the following statements in the Log window.

> NOTE: The data set WORK.OLD1 has 4 observations and 3 variables.
NOTE: The data set WORK.OLD2 has 4 observations and 3 variables.

- 2. Return to the Editor window and add the following statements to the end of this SAS program:

```
DATA NEW; SET OLD1 OLD2; RUN;
PROC PRINT DATA=NEW;RUN;
```

- 3. Run the SAS program and observe the results. The data from the OLD2 data set is appended to the OLD1 data set, and the combined data sets are stored in the NEW set. The results are in the NEW set.

(continued)

- 4. Open the program file DAPPEND2.SAS. Notice that in this program, the data set is the NEW set.

(continued)

- 5. Run the SAS program and observe the results. The data from the OLD2 data set is appended to the OLD1 data set, and the combined data sets are stored in the NEW set. The results are in the NEW set.

# 4.7.2 Merging Data Sets by Key Identifier

Another way to combine data sets is to merge them by a key identifier (It is sometimes called a horizontal merge.) For example, suppose that you have data collected on two occasions, and you want to merge the data sets. 

- 1. Open the program file DMERGE1.SAS. The first data set created in this example is PRE.

```
DATA PRE;
INPUT CASE $PREREAT;
DATALINES;
001 1.02
002 2.10
etc...
```
A second data set in the program is POST:
DATA POST;
INPUT CASE $POSTREAT;
DATALINES;
001 1.94
002 1.63
etc...
```

- 2. Note that each data set contains a variable CASE. This is the key identifier that tells SAS which records to match when performing the merge. Before merging the data sets, you must sort them on the same identifier:

```
PROC SORT DATA=PRE; BY CASE;
PROC SORT DATA=POST; BY CASE;
```

The code opened in SAS is not complete. You must complete the code yourself to make it properly. For example, add the BY CASE; statement to the second PROC SORT. Also, complete the DATA statement in the program to perform the desired merge:

```
DATA PREPOST;
* Create new data set;
MERGE PRE POST; BY CASE;
DIFF=POSTREAT - PREREAT; * Calculate DIFF in new data set;
```

- 3. Run the completed program and observe the results in Table 4.12.

- 4. Make a change to the MERGE statement to rename the variable PREREAT to BASE-LINE.

```
MERGE PRE (RENAME=(PREREAT = BASELINE)) POST;
```
