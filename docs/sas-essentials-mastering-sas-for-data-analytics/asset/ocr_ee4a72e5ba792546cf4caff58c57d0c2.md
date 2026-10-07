# TABLE B.14 January London Fix Gold Prices, Yearly Change

| Obs | YEAR | PRICE | LAG_PRICE | DIFF_PRICE | PCT_INCREASE |
|---|---|---|---|---|-|
| 1 | 2005 | 424.15 | | | - |
| 2 | 2006 | 549.86 | 424.15 | 125.71 | 29.6381 |
| 3 | 2007 | 631.17 | 549.86 | 81.31 | 14.7874 |
| 4 | 2008 | 889.60 | 631.17 | 258.43 | 40.9446 |
| 5 | 2009 | 858.69 | 889.60 | -30.91 | -3.7446 |
| 6 | 2010 | 1117.96 | 858.69 | 259.27 | 30.1937 |
| 7 | 2011 | 1356.40 | 1117.96 | 238.44 | 21.3281 |
| 8 | 2012 | 1656.12 | 1356.40 | 299.72 | 22.0967 |
| 9 | 2013 | 1670.95 | 1656.12 | 14.83 | 0.8955 |
| 10 | 2014 | 1244.80 | 1670.95 | -426.15 | -25.5035 |

# HANDS-ON EXAMPLE (ZIP FUNCTIONS)

A hospital is treating people with a rare disease from all over the world. They want to study the distance patients have to travel for treatment based on the hospital and subject's zip code. The following program calculates distance using ZIP functions.

+   1. Open the program file FUNC_ZIP.SAS.

```
DATA ZIP;
INPUT BEGIN $ END $;
HOSPITAL=ZIPCITY (BEGIN);
SUBJECT=ZIPCITY (END);
DISTANCE=ZIPCITYDISTANCE (BEGIN, END);
DATALINES;
75275 75201
75275 10001
75275 96801
75275 96951
;
PROC PRINT;
RUN;
```

Run this program and the results are given in Table B.15. You can see, for instance, the distance from Honolulu to the hospital in Dallas is 3795 miles.

+   2. You are curious how far it is from the smallest zip code (Holtsville, NY, 00501) to the largest (Ketchikan, AK, 99950). Put those values into the program, run it, and observe the distance. (By the way, the 96951 zip code is for Songong (Rota) Mariana Islands (MP) which is northeast of Guam.

(continued)