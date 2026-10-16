# SQL Code

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL FEEDBACK;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
%MEND DUPS;
%DUPS(WORK,PRODUCTS,PRODTYPE);
```

# SAS Log Results

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL FEEDBACK;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
%MEND DUPS;
%DUPS(WORK,PRODUCTS,PRODTYPE);
NOTE: Statement transforms to:
    select PRODUCTS.prodtype, COUNT(*) as Duplicate_Rows
        from WORK.PRODUCTS
            group by PRODUCTS.prodtype
                having COUNT(*)>1;
```

You can also specify a %PUT statement instead of the FEEDBACK option to display the values of macro variables after macro resolution. The next example illustrates inserting the macro statement %PUT LIB = &LIB TABLE = &TABLE GROUPBY = &GROUPBY between the QUIT and %MEND statements to produce the results illustrated below.

# SQL Code

```
%MACRO DUPS(LIB, TABLE, GROUPBY);
    PROC SQL;
        SELECT &GROUPBY, COUNT(*) AS Duplicate_Rows
            FROM &LIB..&TABLE
                GROUP BY &GROUPBY
                    HAVING COUNT(*) > 1;
    QUIT;
    %PUT LIB = &LIB TABLE = &TABLE GROUPBY = &GROUPBY;
%MEND DUPS;
%DUPS(WORK,PRODUCTS,PRODTYPE);
```