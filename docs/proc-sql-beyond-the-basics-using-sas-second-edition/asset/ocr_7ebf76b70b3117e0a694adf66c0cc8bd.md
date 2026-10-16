# Finding the Length of a String

The LENGTH function is used to obtain the length of a character string column. LENGTH returns a number equal to the number of characters in the argument. Note that the computed column (LENGTH(PRODNAME)) has a column header created for it called Length by specifying the AS keyword. This example illustrates using the LENGTH function to determine the length of data values.

# SQL Code

```
PROC SQL;
    SELECT PRODNUM,
            PRODNAME,
            LENGTH(PRODNAME) AS Length
    FROM PRODUCTS;
QUIT;
```

# Results

| Product Number | Product Name | Length |
|---|---|---|
| 1110 | Dream Machine | 13 |
| 1200 | Business Machine | 16 |
| 1700 | Travel Laptop | 13 |
| 2101 | Analog Cell Phone | 17 |
| 2102 | Digital Cell Phone | 18 |
| 2200 | Office Phone | 12 |
| 5001 | Spreadsheet Software | 20 |
| 5002 | Database Software | 17 |
| 5003 | Wordprocessor Software | 22 |
| 5004 | Graphics Software | 17 |

# Combining Functions and Operators

As in the DATA step, many functions can be used in the SQL procedure. To modify one or more existing rows in a table, the UPDATE statement is used (see Chapter 6, “Modifying and Updating Tables and Indexes,” for more details). The UPDATE statement with the SET clause changes the contents of a data value (functioning the same way as a DATA step assignment statement) by assigning a new value to the column identified to the left of the equal sign by a constant or expression referenced to the right of the equal sign.