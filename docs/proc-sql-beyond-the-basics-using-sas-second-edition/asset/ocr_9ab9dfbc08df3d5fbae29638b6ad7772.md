# SAS Log Results

```
PROC SQL;
CREATE VIEW SOFTWARE_PRODUCTS_VIEW AS
SELECT prodnum, prodname, manunum, prodtype
FROM PRODUCTS
WHERE UPCASE(PRODTYPE) IN ('SOFTWARE');
NOTE: SQL view WORK.SOFTWARE_PRODUCTS_VIEW has been defined.
QUIT;
NOTE: PROCEDURE SQL used:
real time            0.17 seconds
```

The SOFTWARE_PRODUCTS_VIEW view functions just as if it were a base table, although it contains no rows of data. All of the other columns with the exception of the product cost (PRODCOST) column are inherited from the selected columns in the PRODUCTS table. A view determines what columns and rows are processed from the underlying table and, optionally, the SELECT query that references the view can provide additional criteria during processing. In the next example, the view SOFTWARE_PRODUCTS_VIEW is referenced in a SELECT query and arranged in ascending order by product name (PRODNAME).

# SQL Code

```
PROC SQL;
SELECT *
FROM SOFTWARE_PRODUCTS_VIEW
ORDER BY prodname;
QUIT;
```

# Results

| Product Number | Product Name | Manufacturer Number | Product Type |
|---|---|---|---|
| 5002 | Database Software | 500 | Software |
| 5004 | Graphics Software | 500 | Software |
| 5001 | Spreadsheet Software | 500 | Software |
| 5003 | Wordprocessor Software | 500 | Software |

# Hiding Logic Complexities

Because complex logic constructs such as multi-way table joins, subqueries, or hard-to-understand data relationships might be beyond the skill of other staff in your area, you might want to build or customize views so that others can access the information easily. The next example illustrates how