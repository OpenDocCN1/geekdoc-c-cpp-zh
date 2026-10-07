# CHAPTER 6: SAS® ADVANCED PROGRAMMING TOPICS PART 1

(continued)

Note that some STAYHOURS are negative and (if you look at more of the output) values are very large – both positive and negative. It is obvious that some of the dates and times were entered incorrectly. For example, in observation 13, the time left is more than a year after arrival.

If possible you could check original records to reconcile the values. For this exercise, set any negative STAYHOURS or any values greater than 48-h to missing using this code:

```
IF STAYHOURS<0 or STAYHOURS>48 then STAYHOURS=;
```

Submit the program and observe the results.

# 6.4.6 Looking for Duplicate records

A final check for this data set is to determine if there are duplicate records. Typically, this is achieved by looking for duplicate IDs. A simple way to do this is with PROC FREQ. This final example for this section illustrates this process.

# HANDS-ON EXAMPLE

This example shows how to find and count duplicate records.

+   1. Open the program file DISCOVER3.SAS and observe the code. A PROC FREQ is performed on the ID (in this case, the variable SUBJECT). The results are stored in a file named FRECNT (using the OUT=FREQCNT). The NOPRINT tells SAS not to print the frequency table, which might be very large. Finally, the PROC prints only records where COUNT is 2 or more.

```
PROC FREQ data=MYSASLIB.cleaned NOPRINT;
TABLE SUBJECT / OUT=FREQCNT;
RUN;
PROC PRINT DATA=FREQCNT;
WHERE COUNT>1;
RUN;
```

Submit this code and observe the results in Table 6.15. Subject ID=26 is used for two records.

# TABLE 6.15 Discovering Duplicate IDs

| Obs SUBJECT COUNT PERCENT |
|---|---|---|---|
| 26 | 0026 | 2 | 2.5316 |

+   2. Add this code to DISCOVER3.SAS to list only records were SUBJECT=26 .

```
PROC PRINT DATA=MYSASLIB.CLEANED;
WHERE FIND(SUBJECT,"0026");
RUN;
```