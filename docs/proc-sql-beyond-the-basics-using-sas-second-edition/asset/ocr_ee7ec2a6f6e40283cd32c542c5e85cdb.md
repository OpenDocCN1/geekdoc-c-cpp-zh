the HAVING clause restricts what is returned by the SELECT clause to just the manufacturers residing in the state of California.

# SQL Code

```
PROC SQL;
    SELECT PRODNAME,
           PRODTYPE,
           MANUNAME
    FROM PRODUCTS P,
         MANUFACTURERS M
    WHERE P.MANUNUM = M.MANUNUM AND
          CASE PRODTYPE
            WHEN 'Software' THEN 1
            ELSE 0
          END;
QUIT;
```

# Results

![](bbox=[0.18, 0.43, 0.64, 0.6])

# Preventing Division by Zero with a Simple CASE Expression

Division by zero errors can cause many problems for a query, including severe performance degradation. In the next example, a simple CASE expression in a SELECT clause is specified to prevent division by zero errors. Using the INVENTORY table, a CASE expression tells SAS to ignore performing any computations for products containing an INVENQTY value of zero (by assigning a Boolean value of false). Otherwise, the equation INVENCST / INVENQTY is computed and products costing more than $1,000.00 are selected by the WHERE clause. A column heading called, Average_Cost is assigned to the new column with the AS keyword.

# SQL Code

```
PROC SQL;
    SELECT PRODNUM,
           INVENQTY,
           INVENCST,
           CASE INVENQTY
```