# 220 PROC SQL: Beyond the Basics Using SAS, Second Edition



```
PROC SQL;
CREATE TABLE PURCHASES AS
SELECT CUSTNUM, ITEM AS ITEM_PURCHASED, UNITS, UNITCOST
FROM PURCHASES;
QUIT;
```



```
PROC SQL;
CREATE TABLE PURCHASES AS
SELECT CUSTNUM, ITEM AS ITEM_PURCHASED, UNITS, UNITCOST
FROM PURCHASES;
WARNING: This CREATE TABLE statement recursively references the target table. A consequence of this is a possible data integrity problem.
NOTE: Table WORK.PURCHASES created, with 7 rows and 4 columns.
QUIT;
NOTE: PROCEDURE SQL used (Total process time):
real time 0.41 seconds
cpu time 0.02 seconds
```

An alternative approach to renaming columns in a table consists of using the RENAME= SAS data set option in a SELECT statement’s FROM clause. Suppose that you want to rename ITEM in the PURCHASES table to ITEM_PURCHASED. In the next example, the RENAME= SAS data set option can be specified in one of two ways, as illustrated below. Either approach is syntactically correct.



```
PROC SQL;
SELECT *
FROM PURCHASES (RENAME=ITEM=ITEM_PURCHASED) ;
QUIT;
```

< or >



```
PROC SQL;
SELECT *
FROM PURCHASES (RENAME= (ITEM=ITEM_PURCHASED) ) ;
QUIT;
```