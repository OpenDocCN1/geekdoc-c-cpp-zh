# CHAPTER 2: GETTING DATA INTO SAS®

(continued)

+   2. Submit this code and note that the data are read correctly into the defined variables.
The output is given in Table 2.15.

+   3. Add a new record using the city of your choice, making sure to include the correct
dimiter. Resubmit using the code to make sure it works.

TABLE 2.15 Output from
Reading CSV File

| Obs | CITY | STATE | ZIP |
|---|---|---||}{
| 1 | DALLAS | TEXAS | 75208 |
| 2 | LIHUE | HI | 96766 |
| 3 | MALIBU | CA | 90265 |

A more challenging problem is reading in a data set using INPUT where there are blank
values in the data. Consider the following data set. The first three lines represent a ruler
to help you see where the data values are located. (It is NOT part of the data
set.) That is, the last name is in column 01 through 21 (20 characters long). The maximum
length of records is 45 characters.

0 1 2 3 4
0123456789012345678901234567890123456789012345

| | | | | |
|---|---|---|---||}{
| ABRAMS | | C0001 Producer |
| BRISTOW | SYDNEY | C0015 Teacher |
| VAUGHN | MICHAEL | C0033 Agent |
| FLINKMAN | MARSHALL | C0123 Analyst |
| SLOAN | ARVIN | C0666 |
| BRISTOW | | | |
| DIXON | MARCUS | C0233 Chief |

# HANDS-ON EXAMPLE

```
DATA TEST;
FILE "C:\SASDATA\INFILEDAT.TXT";
INPUT LAST $1-21 FIRST $22-30 ID $31-36 ROLE $37-44;
RUN;
PROC PRINT DATA=TEST; RUN;
```

+   1. Open the program file DINFILE4.SAS.

+   2. Submit this code and observe the output. Note that the data are not correct read.
The output is shown in Table 2.16.

A check of the SAS log shows this statement:
nThe minimum record length was 25.
The maximum record length was 44.
NOTE: SAS went to a new line when INPUT statement reached past
t end of a line.