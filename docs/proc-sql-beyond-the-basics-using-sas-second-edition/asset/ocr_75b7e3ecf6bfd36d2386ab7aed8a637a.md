| Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
|---|---|---|---|---|
| 1110 | Dream Machine | 111 | Workstation | $3,200.00 |
| 1200 | Business Machine | 120 | Workstation | $3,300.00 |
| 1700 | Travel Laptop | 170 | Laptop | $3,400.00 |
| 1701 | Travel Laptop SE | . | Laptop | $4,200.00 |
| 2101 | Analog Cell Phone | 210 | Phone | $35.00 |
| 2102 | Digital Cell Phone | 210 | Phone | $175.00 |
| 2200 | Office Phone | 220 | Phone | $130.00 |
| 5001 | Spreadsheet Software | 500 | Software | $299.00 |
| 5002 | Database Software | 500 | Software | $399.00 |
| 5003 | Wordprocessor Software | 500 | Software | $299.00 |
| 5004 | Graphics Software | 500 | Software | $299.00 |
| 6002 | Security Software | . | Software | $375.00 |

# Adding Data with a SELECT Query

You can also add data to a table using a SELECT query with an INSERT INTO statement. A query expression essentially executes an enclosed query by first creating a temporary table and then inserting the contents of the temporary table into the target table being populated. In the process of populating the target table, any columns omitted from the column list are automatically assigned to missing values.

In the next example, a SELECT query is used to add a row of data from the PRODUCTS table into the SOFTWARE_PRODUCTS table. The designated query controls the insertion of data into the target SOFTWARE_PRODUCTS table by using a WHERE clause.

# SQL Code

```
PROC SQL;
    INSERT INTO SOFTWARE_PRODUCTS
        (PRODNUM, PRODNAME, PRODTYPE, PRODCOST)
    SELECT PRODNUM, PRODNAME, PRODTYPE, PRODCOST
        FROM PRODUCTS
        WHERE PRODTYPE IN ('Software') AND
            PRODCOST > 300;
QUIT;
```

The SAS log shows that one row of data was added to the SOFTWARE_PRODUCTS table.