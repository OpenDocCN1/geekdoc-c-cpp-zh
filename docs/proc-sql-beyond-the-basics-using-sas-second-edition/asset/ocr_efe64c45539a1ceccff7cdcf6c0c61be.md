# SQL Code

```
PROC SQL;
    INSERT INTO PRODUCTS
        (PRODNUM, PRODNAME, PRODTYPE, PRODCOST)
        VALUES(6002,'Security Software','Software',375.00)
        VALUES(1701,'Travel Laptop SE', 'Laptop', 4200.00);
    %PUT SQLOBS = &&SQLOBS;
QUIT;
```

# SAS Log Results

```
PROC SQL;
    INSERT INTO PRODUCTS
        (PRODNUM, PRODNAME, PRODTYPE, PRODCOST)
        VALUES(6002,'Security Software','Software',375.00)
        VALUES(1701,'Travel Laptop SE', 'Laptop', 4200.00);
NOTE: 2 rows were inserted into WORK.PRODUCTS.
%PUT SQLOBS = &&SQLOBS;
SQLOBS = 2
QUIT;
```

# SQLLOOPS Macro Variable

The SQLLOOPS macro variable displays the number of times that the inner loop is processed by the SQL procedure. To display the contents of the SQLLOOPS macro variable in the SAS log, specify a %PUT macro statement. The following example retrieves the software products from the PRODUCTS table and displays SAS output with a SELECT statement. The %PUT statement displays the number of times the inner loop is processed as 15 times even though there are only 10 product rows. As a query becomes more complex, the number of times the inner loop of the SQL procedure processes also increases proportionally.

# SQL Code

```
PROC SQL;
    SELECT *
    FROM PRODUCTS
        WHERE PRODTYPE='Software';
%PUT SQLLOOPS = &&SQLLOOPS;
QUIT;
```

# SAS Log Results

```
PROC SQL;
    SELECT *
    FROM PRODUCTS
        WHERE PRODTYPE='Software';
%PUT SQLLOOPS = &&SQLLOOPS;
SQLLOOPS = 15
QUIT;
```