# Results

| Row_Count |
|---:|
| 57 |

Unlike the COUNT(*) function syntax that counts all rows, whether data is missing or not, the next example uses the COUNT function with the (column-name) argument to produce a total number of non-missing rows based on the UNITS column.

# SQL Code

```
PROC SQL;
    SELECT COUNT(UNITS) AS Non_Missing_Row_Count
        FROM PURCHASES;
QUIT;
```

# Results

| Non_Missing_Row_Count |
|---:|
| 57 |

The MIN summary function can be specified to determine what the least expensive product is in the PRODUCTS table.

# SQL Code

```
PROC SQL;
    SELECT MIN(prodcost) AS Cheapest
        Format=dollar9.2 Label=’Least Expensive’
        FROM PRODUCTS;
QUIT;
```

# Results

| Least Expensive |
|---:|
| $35.00 |

In the next example, the SUM function is specified to sum numeric data types for a selected column. Suppose you want to determine the total costs of all purchases by customers who bought workstations (PRODNUM=1110 and 1200) and laptops (PRODNUM=1700). You could construct the following query to sum all non-missing values for customers who purchased workstations and laptops in the PURCHASES table.