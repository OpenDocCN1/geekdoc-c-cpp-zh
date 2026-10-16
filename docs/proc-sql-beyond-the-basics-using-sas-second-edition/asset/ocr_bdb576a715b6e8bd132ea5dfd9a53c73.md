# Results

| prodnum | invenqty |
| --- | --- |
| 5001 | Low on Stock - Reorder |
| 5002 | Low on Stock - Reorder |
| 5001 | Low on Stock - Reorder |
| 1700 | Stock Levels OK |
| 5003 | Stock Levels OK |
| 1110 | Plenty of Stock |
| 5004 | Plenty of Stock |

The same results can also be derived using a CASE expression in the SQL procedure. In the next example, a CASE expression is constructed using the INVENTORY table to assign values to the user-defined column Inventory_Status. The biggest difference between the FORMAT procedure approach and a CASE expression is that the latter uses one step and does not replace the actual data value with the recoded result. Instead, it creates a new column that contains the result of the CASE expression.

# SQL Code

```
PROC SQL;
    SELECT PRODNUM,
        CASE
            WHEN INVENQTY LE 5
                THEN 'Low on Stock - Reorder'
            WHEN 6 LE INVENQTY LE 10
                THEN 'Stock Levels OK'
            WHEN 11 LE INVENQTY LE 99
                THEN 'Plenty of Stock'
            ELSE 'Excessive Quantities'
        END AS Inventory_Status
    FROM INVENTORY
    ORDER BY INVENQTY;
QUIT;
```