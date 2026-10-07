# GOING DEEPER: MORE TECHNIQUES FOR ENTERING DATA 43

+   2. Submit this code, The PROC PRINT produces the output shown in Table 2.14.
3. Change the OBS=11 statement to read in the first 25 records of the data set and rerun the program. (Recall that the first data record is on line 2.)
4. Suppose you only want to read in records 6 through 31. Change the FIRSTOBS and OBS statements to read in only those records and rerun the program. (Recall that record 6 begins on line 7).

# TABLE 2.14 Output from Reading CSV File

| Obs | GROUP | AGE | TIME1 | TIME2 | TIME3 | Time4 | SOCIO |
|---|---|---|---|---|---|---||}{
| 1 | A | 12 | 25.3 | 28.2 | 30.6 | | 5 |
| 2 | A | 11 | 22.8 | 27.5 | 33.3 | 35.8 | 5 |
| 3 | B | 12 | 22.8 | 30.0 | 32.8 | 31.0 | 4 |
| 4 | A | 12 | 18.5 | 26.0 | 29.0 | 27.9 | 5 |
| 5 | B | 9 | 19.5 | 25.0 | 26.3 | 26.6 | 5 |
| 6 | B | 11 | 23.5 | 28.8 | 34.2 | 35.6 | 5 |
| 7 | C | 8 | 22.6 | 26.7 | 28.0 | 33.4 | 3 |
| 8 | B | 8 | 21.0 | 26.7 | 27.5 | 29.5 | 5 |
| 9 | B | 7 | 20.9 | 28.9 | 29.7 | 25.9 | 2 |
| 10 | A | 11 | 22.5 | 29.3 | 32.6 | 33.7 | 2 |

The DLM option allows you to define the delimiter in the data. The following example illustrates how to use this option when there is an unusual delimiter.

# HANDS-ON EXAMPLE

+   1. Open the program file DINFILE3.SAS.

```
DATA PLACES;
INFILE DATALINES DLM='!|~!';
INPUT CITY$ STATE ZIP;
ALALINES;
DALLAS!~TEXAS!~!75208
LIHUE!~HI!~!196766
MALIBU!~CA!~190265
;
PROC PRINT;
RUN;
```

The data are within this code so you can easily see the delimiter, and in case the INFILE DLMSTR= options occur in the INFILE statement, and DATALINES statement tells SAS how to read the data from the DATALINES statement.

(continued)