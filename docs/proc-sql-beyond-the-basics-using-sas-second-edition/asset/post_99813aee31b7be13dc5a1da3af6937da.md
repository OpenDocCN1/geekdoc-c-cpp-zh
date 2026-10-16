
## SQL Code
```
PROC SQL;
    SELECT MANUNAME,
            MANUSTAT,
            CASE MANUSTAT
                WHEN 'CA' THEN 'West'
                WHEN 'FL' THEN 'East'
                WHEN 'TX' THEN 'Central'
                ELSE 'Unknown'
            END AS Region
    FROM MANUFACTURERS;
QUIT;
```

## Results

The SAS System

| Manufacturer Name | Manufacturer State | Region |
|---|---|---|
| Cupid Computer | TX | Central |
| Global Comm Corp | CA | West |
| World Internet Corp | FL | East |
| Storage Devices Inc | CA | West |
| KPL Enterprises | CA | West |
| San Diego PC Planet | CA | West |

The next example illustrates the process of classifying products with a simple CASE expression in a SELECT clause. The PRODTYPE column from the PRODUCTS table is used to assign a character value of “Hardware,” “Software,” or “Unknown” to each product type (e.g., Laptop, Phone, Software, and Workstation). Similar to the assignment process in the FORMAT procedure, new data values are associated with values in the PRODTYPE column. The WHEN-THEN conditions equate “Laptop” to “Hardware,” “Phone” to “Hardware,” “Software” to “Software,” and “Workstation” to “Hardware.” A value of “Unknown” is assigned to products not matching any of the WHEN-THEN logic conditions. Finally, a column heading of Product_Classification is assigned to the new column with the AS keyword.

## SQL Code
```
PROC SQL;
    SELECT PRODNAME,
            CASE PRODTYPE
```
```
END AS Product_Classification
FROM PRODUCTS
ORDER BY PRODNUM;
QUIT;
```

## Results

| Product Name | Product Number | Product_Classification |
|---|---:|---|
| Dream Machine | 1110 | Laptop/Workstation |
| Business Machine | 1200 | Laptop/Workstation |
| Travel Laptop | 1700 | Laptop/Workstation |
| Analog Cell Phone | 2101 | Phone |
| Digital Cell Phone | 2102 | Phone |
| Office Phone | 2200 | Phone |
| Spreadsheet Software | 5001 | Software |
| Database Software | 5002 | Software |
| Wordprocessor Software | 5003 | Software |
| Graphics Software | 5004 | Software |

The next example applies a subquery (for more information, see the “Subqueries” section in Chapter 7, “Coding Complex Queries”) to subset software products from the Product_Classification results created in the previous example.

## SQL Code
```
PROC SQL;
    SELECT *
        FROM
            (SELECT PRODNAME,
                    PRODNUM,
                    CASE SUBSTR(PUT(PRODNUM,4.),1,1)
                        WHEN '1' THEN 'Laptop/Workstation'
                        WHEN '2' THEN 'Phone'
                        WHEN '5' THEN 'Software'
                        ELSE 'Unknown'
```
```
END AS Product_Classification
FROM PRODUCTS
)
WHERE Product_Classification = 'Software';
QUIT;
```

## Results

| Product Name | Product Number | Product_Classification |
|---|---|---|
| Spreadsheet Software | 5001 | Software |
| Database Software | 5002 | Software |
| Wordprocessor Software | 5003 | Software |
| Graphics Software | 5004 | Software |

## Simple CASE Expression in a WHERE Clause

In the previous section, we examined the syntax and application of simple CASE expressions in a SELECT clause. In this section, we’ll explore the syntax and application of simple CASE expressions in a WHERE clause. Because the SQL procedure supports the use of a CASE expression anywhere an expression can be used, we’ll learn that a query can benefit from the capabilities of passing a result value from a CASE expression directly to a WHERE clause in place of a hardcoded value.

## SQL Code
```
PROC SQL;
    SELECT MANUNAME,
        MANUSTAT
    FROM MANUFACTURERS
    WHERE CASE MANUSTAT
        WHEN 'CA' THEN 1
        ELSE 0
    END;
QUIT;
```

## Results

| Manufacturer Name | Manufacturer State |
|---|---|
| Global Comm Corp | CA |
| Storage Devices Inc | CA |
| KPL Enterprises | CA |
| San Diego PC Planet | CA |

## Creating a Customized List with a Simple CASE Expression

A customized display and order can be coded using a simple CASE expression in a SELECT and ORDER BY clause. The following example illustrates a unique way to create a list of products and availability by coding individual Case logic for each product in the PRODUCTS table. The resulting output displays a value of “1” to indicate that it contributed to the output list, or a value of “0” to indicate that it didn’t contribute to the output list.

## SQL Code
```
OPTIONS LS=120;
PROC SQL;
SELECT PRODNAME,
    PRODCOST,
    CASE PRODTYPE WHEN 'Laptop'      THEN 1 ELSE 0 END
        AS LaptopRequest,
    CASE PRODTYPE WHEN 'Workstation' THEN 1 ELSE 0 END
        AS WorkstationRequest,
    CASE PRODTYPE WHEN 'Phone'       THEN 1 ELSE 0 END
        AS PhoneRequest,
    CASE PRODTYPE WHEN 'Software'    THEN 1 ELSE 0 END
        AS SoftwareRequest
FROM PRODUCTS
ORDER BY CASE PRODTYPE WHEN 'Laptop'      THEN 1 ELSE 0 END,
    CASE PRODTYPE WHEN 'Workstation' THEN 1 ELSE 0 END,
    CASE PRODTYPE WHEN 'Phone'       THEN 1 ELSE 0 END,
    CASE PRODTYPE WHEN 'Software'    THEN 1 ELSE 0 END;
QUIT;
```

## Results

| Product Name | Product Cost | LaptopRequest | WorkstationRequest | PhoneRequest | SoftwareRequest |
|---|---:|---:|---:|---:|---:|
| Wordprocessor Software | $299.00 | 0 | 0 | 0 | 1 |
| Graphics Software | $299.00 | 0 | 0 | 0 | 1 |
| Spreadsheet Software | $299.00 | 0 | 0 | 0 | 1 |
| Database Software | $399.00 | 0 | 0 | 0 | 1 |
| Office Phone | $130.00 | 0 | 0 | 1 | 0 |
| Digital Cell Phone | $175.00 | 0 | 0 | 1 | 0 |
| Analog Cell Phone | $35.00 | 0 | 0 | 1 | 0 |
| Dream Machine | $3,200.00 | 0 | 1 | 0 | 0 |
| Business Machine | $3,300.00 | 0 | 1 | 0 | 0 |
| Travel Laptop | $3,400.00 | 1 | 0 | 0 | 0 |

## Simple CASE Expression in a HAVING Clause

A HAVING clause is used in an SQL query to filter out aggregates specified in a GROUP BY clause. In this example, the SELECT clause returns the names of the manufacturers along with their state of residence from the MANUFACTURERS table. The CASE expression in the HAVING clause restricts what is returned by the SELECT clause to only the manufacturers residing in the state of California.

## SQL Code
```
PROC SQL;
    SELECT MANUNAME,
           MANUSTAT
    FROM MANUFACTURERS
    HAVING CASE MANUSTAT
           WHEN 'CA' THEN 1
           ELSE 0
           END;
QUIT;
```

## Results

The SAS System

| Manufacturer Name | Manufacturer State |
|---|---|
| Global Comm Corp | CA |
| Storage Devices Inc | CA |
| KPL Enterprises | CA |
| San Diego PC Planet | CA |

In the next example, the SELECT clause returns the most expensive product(s) from the PRODUCTS table, and the CASE expression in the HAVING clause restricts the results to software products costing more than $300.00.

## SQL Code
```
PROC SQL;
    SELECT PRODNAME,
            PRODTYPE,
            MAX(PRODCOST) AS Product_Cost FORMAT=DOLLAR10.2
    FROM PRODUCTS
    HAVING CASE PRODTYPE
            WHEN 'Software' THEN PRODCOST
            ELSE 0
        END > 300;
QUIT;
```

## Results

The SAS System

| Product Name | Product Type | Product_Cost |
|---|---|---|
| Database Software | Software | $3,400.00 |

## Simple CASE Expression in a Join Construct

A CASE expression can be specified in a JOIN construct to filter out aggregates specified in a GROUP BY clause. In this example, the SELECT clause returns the names of the manufacturers along with their state of residence from the MANUFACTURERS table. The CASE expression in
the HAVING clause restricts what is returned by the SELECT clause to just the manufacturers residing in the state of California.

## SQL Code
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

## Results

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_154_0.png)

## Preventing Division by Zero with a Simple CASE Expression

Division by zero errors can cause many problems for a query, including severe performance degradation. In the next example, a simple CASE expression in a SELECT clause is specified to prevent division by zero errors. Using the INVENTORY table, a CASE expression tells SAS to ignore performing any computations for products containing an INVENQTY value of zero (by assigning a Boolean value of false). Otherwise, the equation INVENCST / INVENQTY is computed and products costing more than $1,000.00 are selected by the WHERE clause. A column heading called, Average_Cost is assigned to the new column with the AS keyword.

## SQL Code
```
PROC SQL;
    SELECT PRODNUM,
           INVENQTY,
           INVENCST,
           CASE INVENQTY
```
