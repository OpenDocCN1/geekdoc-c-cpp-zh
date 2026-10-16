
### SQL Code

```
PROC SQL;
    SELECT
        PRODNUM,
        UNITS,
        UNITCOST,
        UNITS * UNITCOST
            AS Purchase_Amount
            FORMAT=DOLLAR12.2,
        CASE
            WHEN CALCULATED
    Purchase_Amount < 1000 THEN 'Small Purchase'
            WHEN CALCULATED
    Purchase_Amount BETWEEN 1000 AND 7500 THEN 'Average Purchase'
            WHEN CALCULATED
    Purchase_Amount > 7500 THEN 'Large Purchase'
            ELSE 'Unknown Purchase'
        END AS Type_of_Purchase
        FROM PURCHASES
            ORDER BY CALCULATED
    Purchase_Amount DESC;
QUIT;
```

### Results

| Manufacturer Name | Manufacturer State | Region |
|---|---|---|
| Cupid Computer | TX | Central |
| Global Comm Corp | CA | West |
| World Internet Corp | FL | East |
| Storage Devices Inc | CA | West |
| KPL Enterprises | CA | West |
| San Diego PC Planet | CA | West |

## Complex Comparisons with Searched CASE Expressions

As described earlier, searched CASE expressions provide SQL users with the capability to perform more complex comparisons. Combined with logical and comparison operators, CASE expressions along with their WHERE clause counterparts provide the capabilities to construct complex logic scenarios. In the next example, a listing of manufacturers and their products are displayed using a searched CASE expression to assign a value of “East” to manufacturers in Florida, “Central” to manufacturers in Texas, “West” to manufacturers in California, and “Unknown” to all other manufacturers in the MANUFACTURERS table. Using the manufacturer’s state of residence (MANUSTAT) column, a CASE expression is constructed to assign the desired value in each row of data. Finally, a column heading of Region is assigned to the new column with the AS keyword.

### SQL Code

```
PROC SQL;
    SELECT MANUNAME,
        CASE
            WHEN MANUSTAT IN ('FL','TX','CA') THEN
                CASE
                    WHEN PRODTYPE IN ('Laptop', 'Workstation') THEN
                        "Computer Hardware Manufacturer"
                    ELSE "Not a Computer Manufacturer"
                END
            ELSE "Unknown Manufacturer"
        END AS ManufacturerType,
        PRODNAME,
        PRODCOST
    FROM MANUFACTURERS M,
        PRODUCTS P
    WHERE M.MANUNUM = P.MANUNUM;
QUIT;
```

### Results

| Manufacturer Name | ManufacturerType | Product Name | Product Cost |
|---|---|---|---|
| Cupid Computer | Computer Hardware Manufacturer | Dream Machine | $3,200.00 |
| Storage Devices Inc | Computer Hardware Manufacturer | Business Machine | $3,300.00 |
| Global Comm Corp | Not a Computer Manufacturer | Analog Cell Phone | $35.00 |
| Global Comm Corp | Not a Computer Manufacturer | Digital Cell Phone | $175.00 |
| KPL Enterprises | Not a Computer Manufacturer | Spreadsheet Software | $299.00 |
| KPL Enterprises | Not a Computer Manufacturer | Database Software | $399.00 |
| KPL Enterprises | Not a Computer Manufacturer | Wordprocessor Software | $299.00 |
| KPL Enterprises | Not a Computer Manufacturer | Graphics Software | $299.00 |

## Creating a Customized List with a Searched CASE Expression

Similar to the simple CASE expression illustrated earlier, a customized display can be specified using a searched CASE expression in a SELECT clause. The following example illustrates a unique way to create a list of products and availability by coding individual Case logic conditions for each product in the PRODUCTS table. The resulting output displays a value of “1” to indicate that it contributed to the output list, or a value of “0” to indicate that it didn’t contribute to the output list.

### SQL Code

```
OPTIONS LS=120;
PROC SQL;
   SELECT PRODNAME,
          PRODCOST,
          CASE WHEN PRODTYPE='Laptop' AND
                    PRODCOST < 1000 THEN 1
               ELSE 0
          END AS InexpensiveLaptop,
          CASE WHEN PRODTYPE='Laptop' AND
                    PRODCOST BETWEEN 1000 AND 2500 THEN 1
               ELSE 0
          END AS MediumPricedLaptop,
          CASE WHEN PRODTYPE='Laptop' AND
                    PRODCOST > 2500 THEN 1
               ELSE 0
          END AS ExpensiveLaptop
      FROM PRODUCTS
      WHERE PRODTYPE='Laptop'
      ORDER BY PRODCOST;
QUIT;
```

### Results

**The SAS System**

| Product Name | Product Cost | InexpensiveLaptop | MediumPricedLaptop | ExpensiveLaptop |
|---|---|---|---|---|
| Travel Laptop | $3,400.00 | 0 | 0 | 1 |

## Another Customized List with a Searched CASE Expression

Extending the features from the previous searched CASE expression example, a customized list is created. In this example, a unique approach is used to create a list of products with their respective inventory quantities. The query performs an equijoin on the PRODUCTS and INVENTORY tables with Case logic conditions nested two levels deep to capture the inventory quantities for each product in the PRODUCTS table.

### SQL Code

```
PROC SQL;
    SELECT PRODNAME,
        P.PRODNUM,
        CASE WHEN SUBSTR(PUT(P.PRODNUM,4.),1,1) = '1' THEN
            CASE WHEN INVENQTY > 0 THEN INVENQTY
            END
        END AS ComputerHardware,
        CASE WHEN SUBSTR(PUT(P.PRODNUM,4.),1,1) = '2' THEN
            CASE WHEN INVENQTY > 0 THEN INVENQTY
            END
        END AS OfficeEquipment,
        CASE WHEN SUBSTR(PUT(P.PRODNUM,4.),1,1) = '5' THEN
            CASE WHEN INVENQTY > 0 THEN INVENQTY
            END
        END AS ComputerSoftware
    FROM PRODUCTS  P,
        INVENTORY  I
    WHERE P.PRODNUM = I.PRODNUM
        ORDER BY PRODNAME;
QUIT;
```

### Results

| Product Name | Product Number | ComputerHardware | OfficeEquipment | ComputerSoftware |
|---|---|---|---|---|
| Database Software | 5002 | . | . | 3 |
| Dream Machine | 1110 | 20 | . | . |
| Graphics Software | 5004 | . | . | 20 |
| Spreadsheet Software | 5001 | . | . | 5 |
| Spreadsheet Software | 5001 | . | . | 2 |
| Travel Laptop | 1700 | 10 | . | . |
| Wordprocessor Software | 5003 | . | . | 10 |

## Case Logic versus COALESCE Expression

A popular convention among SQL programmers is to specify a COALESCE function in an expression to perform Case logic. As described in Chapter 2, “Working with Data in PROC SQL,” the COALESCE function permits a new value to be substituted for one or more missing column values. By specifying COALESCE in an expression, PROC SQL evaluates each argument from left to right for the occurrence of a non-missing value. The first non-missing value found in the list of arguments is returned; otherwise, a missing value, or assigned value, is returned. This approach not only saves programming time, it makes coding constructs simpler to maintain.

Expressing logical expressions in one or more WHEN-THEN/ELSE conditions are frequently easy to code, understand, and maintain. But as the complexities associated with Case logic increase, the amount of coding also increases. In the following example, a simple CASE expression is presented to illustrate how a value of “Unknown” is assigned and displayed when CUSTCITY is missing.

### SQL Code

```
PROC SQL;
    SELECT CUSTNAME,
        CASE
            WHEN CUSTCITY IS NOT NULL THEN CUSTCITY
            ELSE 'Unknown'
        END AS Customer_City
    FROM CUSTOMER;
QUIT;
```

To illustrate the usefulness of the COALESCE function as an alternative to Case logic, the same query can be modified to achieve the same results as before. By replacing the Case logic with a COALESCE expression as follows, the value of CUSTCITY is automatically displayed unless it is missing. In cases of character data, a value of “Unknown” is displayed. This technique makes the COALESCE function a very useful and is a shorthand approach indeed.

In the next example, the FORMAT procedure is used to assign temporary formatted values based on a range of values for INVENQTY. The result from executing this simple three-step (non-SQL procedure) program shows that the actual INVENQTY value is temporarily replaced with the “matched” value in the user-defined format. The FORMAT statement performs a look-up process to determine how the data should be displayed. The actual data value being looked up is not changed (or altered) during the process, but a determination is made as to how its value should be displayed. The BY statement specifies how BY-group processing is to be constructed. The displayed results show the product numbers in relation to their respective inventory quantity status.

### Non-SQL Code

```
PROC FORMAT;
  VALUE INVQTY
    0 - 5 = 'Low on Stock - Reorder'
    6 - 10 = 'Stock Levels OK'
    11 - 99 = 'Plenty of Stock'
    100 - 999 = 'Excessive Quantities';
RUN;

PROC SORT DATA=INVENTORY;
  BY INVENQTY;
RUN;

PROC PRINT DATA=INVENTORY(KEEP=PRODNUM INVENQTY) NOOBS;
  FORMAT INVENQTY INVQTY.;
RUN;
```
