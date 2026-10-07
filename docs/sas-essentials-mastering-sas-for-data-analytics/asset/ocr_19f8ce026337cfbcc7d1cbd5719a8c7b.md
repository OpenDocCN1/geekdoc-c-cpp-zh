# 40 CHAPTER 2: GETTING DATA INTO SAS®

INPUT ID $ SEX $ AGE WT $ SBP DBP BLDCH #3 OBS1 OBS2 OBS3;

or in another order:

INPUT #2 SBP DBP BLDCH #1 ID $ SEX $ AGE WT #3 OBS1 OBS2 OBS3

An advantage of this technique is that you can read the data lines in SAS in any order, specified by the #n. Note that all of these methods require that there be the same number of records for each subject. If there are differing numbers of records per subject, SAS can still read in the data, but that technique is beyond the scope of this book.

An example of a program (DMULTINE. SAS) to read multiple-line data into SAS as the following:

```
DATA MYDATA;
INPUT ID $ SEX $ AGE WT/ SBP DBP BLDCHL/ OBS1 OBS2 OBS3;
DATALINES;
10011 M 15 115
120 80 254
15 65 102
10012 F 25 180
130 70 240
34 120 132
10013 M 89 170
140 100 279
19 89 111
;
PROC PRINT DATA=MYDATA;
RUN;
```

In this case, we use the / indicator technique to read the three data lines per person. The output for this program is given in Table 2.11. Note that even though there are nine lines of data, the DATA steps reads in the data as three records.

# TABLE 2.11 Multiline Entry

| Obs ID | AGE WT SBP DBP BLDCHL OBS1 OBS2 OBS3 |
|---|---|---|---|---|---|---|---||
| 1 | 10011 M | 15 115 | 120 | 80 | 254 | 15 | 65 | 102 |
| 2 | 10012 F | 25 180 | 130 | 240 | 34 | 120 | 132 |
| 3 | 10013 M | 89 170 | 140 | 100 | 279 | 19 | 89 | 111 |

# HANDS-ON EXAMPLE

+   1. Open the program file DMULTINE.SAS . Change the INPUT line to read in data using each of the three different INPUT statements technique.
2. Change in the INPUT line to read in data using line number technique, but read in first line #1, then line #3, and finally line two #2. Submit the code and observe the output.