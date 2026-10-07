The from and to variables are SAS date values. The 'interval' argument can be one of the following lengths of time:

+   - DAY
- WEEKDAY
- WEEK
- TENDAY
- SEMIMONTH
- MONTH
- QTR
- SEMIY
- YEAR

Thus, the following function counts the number of years between the date variables BEGATE and ENDDATE because the date interval indicated is 'YEAR'.

```
INTCK('YEAR', BEGATE, ENDDATE)
```

The following code counts the number of months between these two dates because the date interval indicated is 'MONTH'.

```
INTCK('MONTH', BEGATE, ENDDATE)
```

Another handy date function is the MDY function. This allows you to convert numbers into a SAS date value. For example:

```
BDATE = MDY(10, 12, 1989);
```

converts the October 12, 1989, into a SAS date value. Dates must be in SAS date format for you to use other SAS date functions or to output dates using SAS format specifications. Or if in a data set you have these values

```
MTH=5; DAY=9; YR=2016;
```

the MDY function

```
VISIDATE = MDY(MTH, DAY, YR);
```

creates a SAS variable named VISIDATE with the value May 9, 2016. For a more comprehensive list of functions, refer to Appendix B in this book.

HANDS-ON EXAMPLE
This example illustrates a method for calculating the difference between two dates (AGE) using the INTCK function. The procedure uses these steps:
1. Read in BDATE as a SAS date value using the INFORMAT MMYYDD8. specification in the INPUT statement.
(continued)