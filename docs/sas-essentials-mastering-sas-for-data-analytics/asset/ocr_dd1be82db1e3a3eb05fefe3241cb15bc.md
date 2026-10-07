# EXERCISES 47

| Variable Name | Column | Type |
| --- | --- | --- |
| ID | 1-5 | Text |
| AGE | 6-7 | Numeric |
| GENDER | 8 | Text (M or F) |
| MARRIED | 9 | Text (Y or N) |
| WEIGHT IN POUNDS | 10-12 | Numeric |

+   a. The SAS code snippet given below using the column input technique.
```sas
DATA PEOPLE;
ID $ 1-5 ; * finish INPUT statement;
DATALINES;
000123MY201
000214FY154
000433FN133
000529MN173
001329FY114
;
Title "Exercise 2.2 - your name";
PROC PRINT DATA=PEOPLE;
RUN;
```

+   b. Run the program. Verify that the input output lists the data correctly.

# 2.3 Complete the INPUT statement using formatted input.

The SAS program EX_2.3.SAS contains a data file with the following columns:

| Variable Name | Column | Type |
| --- | --- | --- |
| ID | 1-5 | Text |
| GENDER | 6 | Text (M or F) |
| MARRIED | 7 | Numeric 0,1 |
| BDATE | 8-16 | Date |

+   a. The SAS code snippet given below using the formatted input technique.
Refer to Table 2.4 to determine which FORMAT to use. For the output FORMAT, use the format that outputs dates in the Thursday, November 23, 2016.

```
DATA BIRTHDATES;
INPUT ID $ 1-5 ; * finish INPUT statement;
BDATE someformat.; * finish OUTPUT FORMAT statement;
DATALINES;
0001M12JAN1999
0002F003MAR1999
0004F018JUL1991
0005M022DEC1998
00132F110JUL1992
;
```