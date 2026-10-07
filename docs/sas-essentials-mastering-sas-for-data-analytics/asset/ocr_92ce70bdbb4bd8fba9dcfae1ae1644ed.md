488  APPENDIX B: SAS® FUNCTION REFERENCE

(continued)

+   2. Add these lines after the BDATEMON line. Rerun the program and observe the output.

```
BDAY=DAY(BDATE);
BYEAR=YEAR(BDATE);
```

This illustrates how to extract various components from a date.

TABLE B.13 Convert Dates to Components

| Obs | BDATE | BDATEDOW | BDATEMONTH |
|---|---|---|--|
| 1 | Sun. Aug 21, 2016 | Sunday | August |
| 2 | Thu, Jul 4, 1776 | Thursday | July |
| 3 | Mon, Jan 1, 1900 | Monday | January |

# HANDS-ON EXAMPLE (LAG)

+   1. Open the program file FUNC_LAG.SAS. This program uses the LAG function to calculate the difference in price of gold from the previous year. Run this program and observe the results in Table B.14.

```
DATA PRICE;
INPUT YEAR PRICE;
LAG_PRICE = LAG(PRICE);
DIFF_PRICE = PRICE - LAG_PRICE;
PCT_INCREASE = (DIFF_PRICE/LAG_PRICE)*100;
DATALINES;
2005 524.15
2006 549.86
2007 631.17
2008 889.60
2009 888.69
2010 1117.96
2011 1356.40
2012 1656.12
2013 1670.95
2014 1244.80
;
RUN;
PROC PRINT;RUN;
```

+   2. Change the LAG function to LAG2 to find the 2-year changes. Rerun the program and observe the output.