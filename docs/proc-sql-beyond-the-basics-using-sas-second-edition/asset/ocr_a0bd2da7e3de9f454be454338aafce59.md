# SAS Log Results

```
PROC SQL NOPRINT;
    SELECT MIN(PRODCOST) FORMAT=DOLLAR10.2
        INTO :MIN_PRODCOST
        FROM SQL.PRODUCTS;
QUIT;
NOTE: PROCEDURE SQL used:
      real time          0.05 seconds

%PUT &MIN_PRODCOST;
$35.00
```

# Creating Multiple Macro Variables

PROC SQL enables you to create a macro variable for each row returned by a SELECT statement. Using the PROC SQL keyword THROUGH or hyphen (-) with the INTO clause, a range of two or more macro variables is easily created. This is a handy feature for creating macro variables from multiple rows in a table. For example, suppose we want to create macro variables for the three least expensive products in the PRODUCTS table. The INTO clause creates three macro variables and assigns values from the first three rows of the PRODNAME and PRODCOST columns. The ORDER BY clause is also specified to perform an ascending sort on product cost (PRODCOST) to assure that the data is in the desired order from least to most expensive. The results are displayed in the SAS log.

# SQL Code

```
PROC SQL NOPRINT;
    SELECT PRODNAME,
           PRODCOST
        INTO :PRODUCT1 - :PRODUCT3,
             :COST1 - :COST3
        FROM PRODUCTS
        ORDER BY PRODCOST;
QUIT;
%PUT &PRODUCT1 &COST1;
%PUT &PRODUCT2 &COST2;
%PUT &PRODUCT3 &COST3;
```