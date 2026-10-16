
displayed and, when multiple names for the same function are available, the ANSI-approved name appears first.

| Summary Function | Description |
| --- | --- |
| AVG, MEAN | Average or mean of values |
| COUNT, FREQ, N | Aggregate number of non-missing values |
| CSS | Corrected sum of squares |
| CV | Coefficient of variation |
| MAX | Largest value |
| MIN | Smallest value |
| NMISS | Number of missing values |
| PRT | Probability of a greater absolute value of Student's t |
| RANGE | Difference between the largest and smallest values |
| STD | Standard deviation |
| STDERR | Standard error of the mean |
| SUM | Sum of values |
| SUMWGT | Sum of the weight variable values which is 1 |
| T | Testing the hypothesis that the population mean is zero |
| USS | Uncorrected sum of squares |
| VAR | Variance |

The next example uses the COUNT function with the (*) argument to produce a total number of rows, whether data is missing or not. The asterisk (*) is specified as the argument to the COUNT function to count all rows in the PURCHASES table.

### SQL Code

```
PROC SQL;
    SELECT COUNT(*) AS Row_Count
    FROM PURCHASES;
QUIT;
```

### Results

| Row_Count |
|---:|
| 57 |

Unlike the COUNT(*) function syntax that counts all rows, whether data is missing or not, the next example uses the COUNT function with the (column-name) argument to produce a total number of non-missing rows based on the UNITS column.

### SQL Code

```
PROC SQL;
    SELECT COUNT(UNITS) AS Non_Missing_Row_Count
        FROM PURCHASES;
QUIT;
```

### Results

| Non_Missing_Row_Count |
|---:|
| 57 |

The MIN summary function can be specified to determine what the least expensive product is in the PRODUCTS table.

### SQL Code

```
PROC SQL;
    SELECT MIN(prodcost) AS Cheapest
        FORMAT=DOLLAR9.2 LABEL='Least Expensive'
        FROM PRODUCTS;
QUIT;
```

### Results

| Least Expensive |
|---:|
| $35.00 |

In the next example, the SUM function is specified to sum numeric data types for a selected column. Suppose you want to determine the total costs of all purchases by customers who bought workstations (PRODNUM=1110 and 1200) and laptops (PRODNUM=1700). You could construct the following query to sum all non-missing values for customers who purchased workstations and laptops in the PURCHASES table.

### SQL Code

```
PROC SQL;
    SELECT SUM((UNITS) * (UNITCOST))
        AS Total_Purchases FORMAT=DOLLAR12.2
        FROM PURCHASES
        WHERE PRODNUM = 1110 OR
              PRODNUM = 1200 OR
              PRODNUM = 1700;
QUIT;
```

### Results

| Total_Purchases |
|-----------------|
| $237,500.00     |

Data can also be summarized down rows (observations) as well as across columns (variables). This flexibility gives SAS users an incredible range of power, and the ability to take advantage of several summary functions that are supplied (or built-in) by SAS. These techniques permit the average of quantities rather than the set of all quantities. Without the ability to summarize data in PROC SQL, users would be forced to write complicated formulas and/or routines, or even write and test DATA step programs to summarize data. Two examples will be illustrated to show how SQL can be constructed to summarize data:

- Summarizing data down rows
- Summarizing data across columns

## Summarizing Data Down Rows

The SQL procedure can be used to produce a single aggregate value by summarizing data down rows (or observations). The advantages of using a summary function in PROC SQL is that it will generally compute the aggregate quicker than if a user-defined equation were constructed, and it saves the effort of having to construct and test a program containing the user-defined equation in the first place. Suppose you want to know the average product cost for all software in the PRODUCTS table containing a variety of products. The following query computes the average product cost and produces a single aggregate value using the AVG function.

### SQL Code

```
PROC SQL;
    SELECT AVG(PRODCOST) AS
        AVERAGE_PRODUCT_COST FORMAT=DOLLAR10.2
        FROM PRODUCTS
        WHERE UPCASE(PRODTYPE) IN
            ("SOFTWARE");
QUIT;
```

### Results

| AVERAGE_PRODUCT_COST |
| --- |
| $324.00 |

## Summarizing Data Across Columns

When a computation is needed on two or more columns in a row, the SQL procedure can be used to summarize data across columns. Suppose you want to know the average cost of products in inventory. The next example computes the average inventory cost for each product without using a summary function, and once computed displays the value for each row as AVERAGE_PRICE.

### SQL Code

```
PROC SQL;
SELECT PRODNUM,
    (INVPRICE / INVQTY) AS
        AVERAGE_PRICE
        FORMAT=DOLLAR8.2
FROM INVOICE;
QUIT;
```

### Results

| Product Number | AVERAGE_PRICE |
| --- | --- |
| 5001 | $299.00 |
| 6001 | $799.00 |
| 2101 | $35.00 |
| 1110 | $3200.00 |
| 5002 | $399.00 |
| 6000 | $99.00 |
| 1200 | $3300.00 |

## Predicates

Predicates are used in PROC SQL to perform direct comparisons between two conditions or expressions. Six predicates will be looked at:

- BETWEEN
- IN
- IS NULL
- IS MISSING
- LIKE
- EXISTS

### Selecting a Range of Values

The BETWEEN predicate is a way of simplifying a query by selecting column values within a designated range of values. BETWEEN is equivalent to an AND combination of one LE (less than or equal) and one GE (greater than or equal) conditions; inclusive of both endpoints. It is extremely flexible because it works with character, numeric, and date values. Programmers can also combine two or more BETWEEN predicates with AND or OR operators for more complicated conditions. In the next example, a range of products costing between $200.00 and $500.00 inclusively are selected from the PRODUCTS table.

### SQL Code

```
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            PRODCOST
        FROM PRODUCTS
        WHERE PRODCOST BETWEEN 200 AND 500;
QUIT;
```

### Results

| Product Name | Product Type | Product Cost |
|---|---|---|
| SpreadsheetSoftware | Software | $299.00 |
| DatabaseSoftware | Software | $399.00 |
| WordprocessorSoftware | Software | $299.00 |
| GraphicsSoftware | Software | $299.00 |

In the next example, products are selected from the INVENTORY table that were ordered between the years 1999 and 2000. The YEAR function returns the year portion from a SAS date value and is used as the range of values in the WHERE clause.

### SQL Code

```
PROC SQL;
    SELECT PRODNUM,
            INVENQTY,
            ORDDATE
        FROM INVENTORY
        WHERE YEAR(ORDDATE) BETWEEN 1999 AND 2000;
QUIT;
```

### Results

| Product Number | Inventory Quantity | Date Inventory Last Ordered |
|---|---|---|
| 1110 | 20 | 09/01/2000 |
| 1700 | 10 | 08/15/2000 |
| 5001 | 5 | 08/15/2000 |
| 5002 | 3 | 08/15/2000 |
| 5003 | 10 | 08/15/2000 |
| 5004 | 20 | 09/01/2000 |
| 5001 | 2 | 09/01/2000 |

The BETWEEN predicate and OR operator are used together in the next example to select products ordered between 1999 and 2000 or where inventory quantities are greater than 15. The YEAR function returns the year portion from a SAS date value and is used as the range of values in the WHERE clause.

### SQL Code

```
PROC SQL;
    SELECT PRODNUM,
            INVENQTY,
            ORDDATE
    FROM INVENTORY
    WHERE (YEAR(ORDDATE) BETWEEN 1999 AND 2000) OR
            INVENQTY > 15;
QUIT;
```

### Results

| Product Number | Inventory Quantity | Date Inventory Last Ordered |
|---|---|---|
| 1110 | 20 | 09/01/2000 |
| 1700 | 10 | 08/15/2000 |
| 5001 | 5 | 08/15/2000 |
| 5002 | 3 | 08/15/2000 |
| 5003 | 10 | 08/15/2000 |
| 5004 | 20 | 09/01/2000 |
| 5001 | 2 | 09/01/2000 |

### Selecting Nonconsecutive Values

The IN predicate selects one or more rows based on the matching of one or more column values in a set of values. The IN predicate creates an OR condition between each value and returns a Boolean value of True if a column value is equal to one or more of the values in the expression list. Although the IN predicate can be specified with single column values, it may be less costly to specify the "=" sign instead. The "=" sign is used in the next example rather than the IN predicate to select phones from the PRODUCTS table.

### SQL Code

```
PROC SQL;
    SELECT PRODNAME,
        PRODTYPE,
        PRODCOST
    FROM PRODUCTS
    WHERE UPCASE(PRODTYPE) = 'PHONE';
QUIT;
```

### Results

| Product Name | Product Type | Product Cost |
|---|---|---|
| AnalogPhone | Phone | $35.00 |
| DigitalPhone | Phone | $175.00 |
| OfficePhone | Phone | $130.00 |
