
# USING IF-THEN-ELSE CONDITIONAL STATEMENT ASSIGNMENTS 83

TABLE 4.7 SAS Logical Operators

| Symbol | Mnemonic | Meaning | Example |
|---|---|---|---|
| & | AND | Both | I>5 AND J<3 |
| | | OR | Either | I>5 OR J<3 |
| ^ OR ~ | NOT | Negate | NOT (I GT J) |

The preceding lines decode the variable (TRT) into a new variable (GROUP). If TRT is equal to A, then GROUP is set to the value 1. If TRT is B or C, GROUP is set to the value 2. Otherwise, GROUP is set to the value 3. A summary of the SAS logical operators is shown in Table 4.7.

# HANDS-ON EXAMPLE

In this example, you will use an IF-THEN-ELSE conditional statement to create a new variable.

- 1. Open the program file DCONDITION.SAS.

```
DATA MYDATA;
INPUT ID $ DBP GENDER $ AGE WT;
IF SB GE 140 THEN STATUS="HIGH"; ELSE STATUS="OK";
DATALINES;
001 120 80 M 15 115
002 130 70 F 25 180
003 140 100 M 89 170
004 180 80 F 30 150
005 125 80 F 20 110
;
PROC PRINT;
RUN;
```

- 2. Notice the IF-THEN-ELSE statement. If systolic blood pressure (SBP) is greater than or equal to 140, the program assigns the value HIGH to the variable STATUS. Otherwise, it assigns the value OK to that variable.

- 3. Run the program and observe the results in Table 4.8.

TABLE 4.8 Results of IF-THEN-ELSE Statement

| Obs | SBP | DBP | GENDER | AGE | WT | STATUS |
|---|---|---|---|---|---|---|
| 1 | 001 | 120 | 80 M | 15 | 115 | OK |
| 2 | 002 | 130 | 70 F | 25 | 180 | OK |
| 3 | 003 | 140 | 100 M | 89 | 170 | HIGH |
| 4 | 004 | 180 | 80 F | 30 | 150 | HIGH |
| 5 | 005 | 125 | 80 F | 20 | 110 | OK |

(continued)

> Notice that the new variable STATUS is assigned either the value OK or the value HIGH depending on the value SBP. Also notice that the first use of the variable STATUS was as a character (text) value, it is set to a SAS character type variable.

## 4.3.1 Using IF-THEN to Assign Values

An IF-THEN statement is a common way to specify missing values in a SAS DATA step. For example,

```
IF AGE = -9 THEN AGE = ;
```

indicates that the value of AGE is equal to –9, the value of AGE is set to a missing value (dot). Because there is no ELSE clause, the value of AGE is not changed when equal to –9. To specify a missing character, use two quotation marks. For example,

```
IF GENDER = "M" AND GENDER NE "F" then GENDER = "";
```

specifies a missing value for GENDER (two quotation marks in a row, "") when it is neither M nor F. A blank (two quotation marks) is a common missing for character variables.

When recoding values using an IF-THEN statement, you need to take care that all possibilities are accounted for. For example, suppose that you are recoding AGE into a new variable TEEN. Use the following code:

```
IF AGE GT 12 AND AGE LT 20 THEN TEEN=1;ELSE TEEN = 0;
IF AGE = . THEN TEEN = .;
```

The use of IF AGE = . THEN TEEN = . guarantees the value of TEEN is set to missing for any observation for which AGE is missing. Otherwise, any observation where AGE is less than 12 and greater than or equal to 20 is coded as TEEN = 0;

## HANDS-ON EXAMPLE

In this example, you will use IF-THEN and IF-THEN-ELSE statements in the DATA step to create a new variable and define a missing value.

- 1. Open the program file DMISS.SAS.

```
DATA MYDATA;
INPUT $ DBP GENDER AGE;
IF AGE GT 12 AND AGE LT 20 THEN TEEN=1;ELSE TEEN = 0;
IF AGE = . THEN TEEN = .;
DATALINES;
001 120 80 M 15
002 130 70 F .
003 140 100 M 12
004 180 80 F 17
005 125 80 F 23
006 165 80 M 18
007 121 80 F 19
008 195 80 M 11
009 162 80 M 13
010 112 80 F 17
;
PROC PRINT;
RUN;
```

- 2. Notice the IF statements that define the new variable TEEN. They also set TEEN to missing (.) IF AGE is missing. Run this program to see that the value of TEEN in the second observation is set to missing.

- 3. Comment the second IF statement by placing an asterisk (*) before it (The line should be displayed in green signifying it is now a comment.) Submit the changed code and observe that the value of TEEN for ID 002 was given the value 0.

- 4. Use the second method described previously to do the same task:

```
IF AGE = . THEN TEEN=
ELSE AGE GT 12 AND AGE LT 20 THEN TEEN=1 ELSE TEEN=0;
```

Submit the program. Did this work correctly?

## 4.3.2 Using IF and IF-THEN to Subset Data Sets

Data sets can be quite large. You may have a data set that contains group of subjects (records) that you want to eliminate from your analysis. In that case, you can subset the data so it will contain only records you need. For example, if your analysis concerns pregnancies, you may want to limit your data set to females.

One method of eliminating certain records from a data set is to use a subsetting IF statement in the DATA step. The syntax for this statement follows:

```
IF expression;
```

where the expression is some conditional in terms of the variables in the data set. For example, to select records containing the value F (only females) from a data set, you could use this statement within a DATA step:

```
IF GENDER EQ 'F';
```

Note that you can use single or double quotation marks ("F" or 'F') in this statement. This subsetting IF statement is similar to a gate. It allows only records that meet a certain criterion to enter into the data set. In this case, only records where GENDER value is recorded as F are retained in the data set.

The opposite effect can be created by including the statement DELETE at the end of the statement:

```
IF expression THEN DELETE;
```

For example, to get rid of certain records (all males) in a data set, you could use the code

```
IF GENDER EQ 'M' THEN DELETE;
```

When a record is read into an SAS data set using this procedure and a record contains M for GENDER, the data is not retained in the data set. If the only values for GENDER in the data set are F and M, these two subsetting strategies will yield the same results.

You are not limited to using the IF statement on character variables. An example that you use the IF statement on a numeric variable is as follows:

```
IF AGE GT 19;
```

You can also use combinations of conditions in any of these IF statements, such as

```
IF AGE GT 19 AND GENDER = "M";
```

> The statement DELETE does not indicate that these records are erased from the raw data file on disk. The records are only eliminated from the SAS data set created in the DATA step.

## HANDS-ON EXAMPLE

In this example, you use a subsetting IF to select only certain records for inclusion in the MYDATA SAS data set created in the DATA step.

- 1. Open the program file DSUBSET1.SAS. In this example, subjects less than or equal to 10 years are included in the data set named MYDATA.

```
DATA MYDATA;
INFILE 'C:\SASDATA\EXAMPLE.DAT';
INPUT ID 1-3 GP $ 5 AGE 6-9 TIME1 10-14 TIME2 15-19;
IF AGE LE 10;
PROC PRINT;
RUN;
```

Notice that the subsetting IF statement selects only records for which AGE is less than or equal to 10. (This does not change the contents of the file C:\SASDATA\EXAMPLE.DAT; it affects only the contents of the new SAS data set MYDATA.)

- 2. Run this program and observe the results. The data listing includes only the 22 subjects whose age is less than or equal to 10.

## 4.3.3 Using IF-THEN and DO for Program Control

Another use of the IF statement is to control the flow of your program in conjunction with a DO statement. In this case, you can assign a group of SAS commands to be executed by using the following type of code:

```
IF expression then DO;
Code to execute;
END;
```

For example, suppose that you want to calculate BMI (Body Mass Index) for subjects in a data set, but the formula is only relevant for subjects older than 19. At the same time, you can assign other values for this group of subjects. You could use the following code:

```
IF AGE GT 19 then DO;
BMI=(WTLBS/HTINCH)**703;
ISADULT=1;
INCLUDESTUD="Yes";
END;
```

In this case, when AGE for a subject older than 19, a series of lines of code is processed. For other subjects in the data set where AGE is younger or equal to 19, BMI, ISADULT, and INCLUDESTUD are not assigned values, and thus have a missing value. (You might have a second IF-THEN-DO statement to assign other values.)

## 4.3.4 Using @ and IF to Conditionally Read Lines in a Data Set

For big data sets, it is often the case that you don't want to read in all of the data. One method you could use to read in certain records is to set a test condition and read in the record only if it meets that condition. To do this, you can use the @ it sign in your input statement to read a portion of a record and put the input on hold while you decide whether or not to read in the complete record. This is referred to as a "trailing at." This is illustrated in the following example:

# HANDS-ON EXAMPLE

This example illustrates the use of a trailing at to conditionally read in data.

- 1. Open the program file DSUBSET.SAS. Note the first INPUT statement ends in a trailing at. The IF statement tests for records where group is A and age is older than equal to 10 reads only the records that matches the condition.

```
DATA MYDATA;
INFILE 'C:\SASDATA\EXAMPLE.DAT';
INPUT GP $5 AGE 6-9 @;
IF GP EQ "A" AND AGE GE 10 THEN
INPUT ID $ 1-3 GP $5 AGE 6-9 TIME1 10-14 TIME2 15-19;
PROC PRINT DATA=MYDATA;
RUN;
```
