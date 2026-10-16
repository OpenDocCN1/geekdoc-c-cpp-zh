view’s WHERE clause after the updates are made. As a result, the view updates the rows with the specified changes, but it is no longer able to display the rows of data that were changed.

Suppose that you want to create a view to select laptops that cost less than $2,800.00 from the PRODUCTS table. The SQL procedure code that is used to create the view called LAPTOP_DISCOUNT_VIEW consists of a SELECT statement with a WHERE clause. There are four defined columns: product number, product name, product type, and product cost, in that order. When accessed, the view produces the results displayed below.

# SQL Code

```
PROC SQL;
    CREATE VIEW LAPTOP_DISCOUNT_VIEW AS
        SELECT PRODNUM, PRODNAME, PRODTYPE, PRODCOST
          FROM PRODUCTS
         WHERE UPCASE(PRODTYPE) = 'LAPTOP' AND
               PRODCOST < 2800.00;
QUIT;
```

# Results

|  | Product Number | Product Name | Product Type | Product Cost |
|---|---|---|---|---|
| 1 | 1700 Travel Laptop | Laptop | $2,720.00 |

The next example illustrates how updates are applied through a view in the Windows environment so that the rows in the table no longer meet the view’s criteria. Suppose that a fifteen percent surcharge is applied to all laptops. An UPDATE statement and SET clause are specified to allow the rows in the PRODUCTS table to be updated through the view. Once the update is performed and the view is accessed, a dialog box appears that indicates that no rows are available to display because the data from the PRODUCTS table no longer meets the view’s WHERE clause expression.

# SQL Code

```
PROC SQL;
    UPDATE LAPTOP_DISCOUNT_VIEW
        SET PRODCOST = PRODCOST + (PRODCOST * 0.15);
QUIT;
```