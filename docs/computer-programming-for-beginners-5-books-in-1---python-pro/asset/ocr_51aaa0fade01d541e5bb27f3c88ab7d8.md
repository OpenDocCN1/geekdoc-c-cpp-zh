form part of the GROUP BY clause.
The syntax would be:

```
SELECT column1, column2, ... "columnN", MIN (<expression>)
FROM table_name;
GROUP BY column1, column2, ... "columnN";
```

To demonstrate how the MIN() function is used in SQL, use the Sales_Rep table with the following data:

| ID | EMP_NAME | SALES | BRANCH |
|---:|---|---:|---|
| 1001 | ALAN MARCH | 3000.00 | NEW YORK |
| 1098 | NEIL BANKS | 5400.00 | LOS ANGELES |
| 2005 | RAIN ALONZO | 4000.00 | NEW YORK |
| 3008 | MARK FIELDING | 3555.00 | CHICAGO |
| 4356 | JENNER BANKS | 14600.00 | NEW YORK |
| 4810 | MAINE ROD | 7000.00 | NEW YORK |
| 5783 | JACK RINGER | 6000.00 | CHICAGO |
| 6431 | MARK TWAIN | 10000.00 | LOS ANGELES |
| 7543 | JACKIE FELTS | 3500.00 | CHICAGO |
| 8934 | MARK GOTH | 5400.00 | AUSTIN |

10 rows in set (0.00 sec)

To get the lowest sales amount, use the following statement:

```
SELECT MIN(Sales) FROM Sales_Rep;
```

The output would be: