# HANDS-ON EXAMPLE

This example illustrates how to summarize counts from a data set into a frequency table.

+   1. Open the program file AFREQ3.SAS.

```
DATA COINS;
INPUT @1 CATEGORY $9. @11 NUMBER 3;
DATALINES;
CENTS 152
CENTS 100
NICKELS 49
DIMES 59
QUARTERS 21
HALF 44
DOLLARS 21;

PROC FREQ WEIGHT NUMBER;
TITLE 'Reading Summarized Count data';
TABLES CATEGORY;
RUN;
```

Note that the data are already in counts. The statement

WEIGHT NUMBER;

tells PROC FREQ that for the variable NUMBER are counts. Even though there are two records for CENTS, the program is able to combine the WEIGHT (counts) into a single CENTS category (252 CENTS).

+   2. Run the program and observe the output for PROC FREQ, as given in Table 10.8.

TABLE 10.8 Simple Output for PROC FREQ
Reading Summarized Count data
\ FREQ Procedure

| CATEGORY | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|---|---|---|---|--|
| CENTS | 252 | 56.50 | 252 | 56.50 |
| DIMES | 59 | 13.23 | 311 | 69.73 |
| DOLLARS | 21 | 4.71 | 332 | 74.44 |
| HALF | 44 | 9.87 | 376 | 84.30 |
| NICKELS | 49 | 10.99 | 425 | 95.29 |
| QUARTERS | 21 | 4.71 | 446 | 100.00 |