
## SAS Log Results

```
PROC SQL;
    CREATE VIEW NO_CAN_DO_VIEW AS
        SELECT *
            FROM NO_CAN_DO_VIEW;
NOTE: SQL view WORK.NO_CAN_DO_VIEW has been defined.
    SELECT *
        FROM NO_CAN_DO_VIEW;
ERROR: The SQL View WORK.NO_CAN_DO_VIEW is referenced recursively.
    QUIT;
NOTE: The SAS System stopped processing this step because of errors.
NOTE: PROCEDURE SQL used (Total process time):
        real time           0.00 seconds
        cpu time            0.01 seconds
```

## Views and SAS Procedures

In most cases but not all, views can be used just as input SAS data sets to the universe of available SAS procedures. In the first example, the INVENTORY_VIEW view is used as input to the MEANS procedure to produce simple univariate descriptive statistics for numeric variables. Accessing the INVENTORY_VIEW view is different from accessing the INVENTORY table because the view’s internal compiled executable statements are processed providing current data from the underlying table to the view itself. The view statements and the statements and options from the MEANS procedure determine what information is produced.

The next example uses the INVENTORY_VIEW view as input to the MEANS procedure to produce simple univariate descriptive statistics for numeric variables. Accessing the INVENTORY_VIEW view is different from accessing the INVENTORY table because the view derives and provides current data from the underlying table to the view itself. The view statements and the statements and options from the MEANS procedure determine what information is produced.

## SAS Code

```
PROC MEANS DATA=INVENTORY_VIEW;
    TITLE1 'Inventory Statistical Report';
    TITLE2 'Demonstration of a View used in PROC MEANS';
RUN;
```

## SAS Log Results

```
PROC MEANS DATA=INVENTORY_VIEW;
TITLE1 'Inventory Statistical Report';
TITLE2 'Demonstration of a View used in PROC MEANS';
RUN;
NOTE: There were 7 observations read from the dataset WORK.INVENTORY.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY_VIEW.
NOTE: PROCEDURE MEANS used:
real time          0.32 seconds
```

## Results

## Inventory Statistical Report
Demonstration of a View used in PROC MEANS
The MEANS Procedure

| Variable | Label | N | Mean | Std Dev | Minimum | Maximum |
| prodnum | Product Number | 7 | 3974.43 | 1763.50 | 1110.00 | 5004.00 |
| invqty | Inventory Quantity | 7 | 10.0000000 | 7.5055535 | 2.0000000 | 20.0000000 |
| invcnst | Inventory Cost | 7 | 11357.14 | 17866.72 | 900.0000000 | 45000.00 |
| AverageAmount |  | 7 | 917.1428571 | 1121.71 | 70.0000000 | 2800.00 |

The next example uses the INVENTORY_VIEW view as input to the PRINT procedure to produce a detailed listing of the values that are contained in the underlying base table.

Note: It is worth noting that, as with all procedures, all procedure options and statements are available by views.

## SAS Code

```
PROC PRINT DATA=INVENTORY_VIEW N NOOBS UNIFORM;
TITLE1 'Inventory Detail Listing';
TITLE2 'Demonstration of a View used in PROC PRINT';
format AverageAmount dollar10.2;
RUN;
```

## SAS Log Results

```
PROC PRINT DATA=INVENTORY_VIEW N NOOBS UNIFORM;
    TITLE1 'Inventory Detail Listing';
    TITLE2 'Demonstration of a View used in a Procedure';
    format AverageAmount dollar10.2;
RUN;
NOTE: There were 7 observations read from the dataset WORK.INVENTORY.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY_VIEW.
NOTE: PROCEDURE PRINT used:
      real time          0.04 seconds
```

## Results

Inventory Detail Listing
Demonstration of a View used in PROC PRINT

| prodnum | invqty | invcnst | AverageAmount |
|---------|--------|---------|---------------|
| 1110    | 20       | $45,000.00 | $2,250.00 |
| 1700    | 10       | $28,000.00 | $2,800.00 |
| 5001    | 5        | $1,000.00  | $200.00 |
| 5002    | 3        | $900.00    | $300.00 |
| 5003    | 10       | $2,000.00  | $200.00 |
| 5004    | 20       | $1,400.00  | $70.00 |
| 5001    | 2        | $1,200.00  | $600.00 |
|         |          | N = 7     |               |

## Views and DATA Steps

As you have already seen, views can be used as input to SAS procedures as if they were data sets. You will now see that views are a versatile component that can be used in a DATA step as well. This gives you a controlled way of using views to access tables of data in custom report programs. The next example uses the INVENTORY_VIEW view as input to the DATA step as if it were a SAS base table. Notice that the KEEP= data set option reads only two of the variables from the INVENTORY_VIEW view.

## SAS Code

```
OPTIONS FORMCHAR="|----|+|----+=|-|\/<>'*";
DATA _NULL_;
    SET INVENTORY_VIEW (KEEP=PRODNUM AVERAGEAMOUNT);
    FILE PRINT HEADER=H1;
    PUT @10 PRODNUM
        @30 AVERAGEAMOUNT DOLLAR10.2;
RETURN;
H1: PUT @9 'Using a View in a DATA Step'
    /// @5 'Product Number'
    @26 'Average Amount';
RETURN;
RUN;
```

## SAS Log Results

```
OPTIONS FORMCHAR="|----|+|----+=|-|\/<>'*";
DATA _NULL_;
    SET INVENTORY_VIEW (KEEP=PRODNUM AVERAGEAMOUNT);
    FILE PRINT HEADER=H1;
    PUT @10 PRODNUM
        @30 AVERAGEAMOUNT DOLLAR10.2;
RETURN;
H1: PUT @9 'Using a View in a DATA Step'
    /// @5 'Product Number'
    @26 'Average Amount';
RETURN;
RUN;
NOTE: 11 lines were written to file PRINT.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY.
NOTE: There were 7 observations read from the dataset WORK.INVENTORY_VIEW.
NOTE: DATA statement used:
      real time          0.00 seconds
```

## Output

Using a View in a DATA Step

Product Number    Average Amount
1110              $2,250.00
1700              $2,800.00
5001              $200.00
5002              $300.00
5003              $200.00
5004              $70.00
5001              $600.00

## Eliminating Redundancy

Data redundancy commonly occurs when two or more users want to see the same data in different ways. To prevent redundancy, organizations should create and maintain a master database environment rather than propagate one or more subsets of data among its user communities. The latter approach creates an environment that is not only problematic for the organization but for its users and customers.

Views provide a way to eliminate or, at least, reduce the degree of data redundancy. Rather than having the same data exist in multiple forms, views create a virtual and shareable database environment for all. Problems that are related to accessing and reporting outdated information, as well as table and program change control, are eliminated.

## Restricting Data Access—Security

As data security issues grow increasingly important for organizations around the globe, views offer a powerful alternative in controlling or restricting access to sensitive information. Views, like tables, can prevent unauthorized users from accessing sensitive portions of data. This is important because security breaches pose great risks not only to an organization’s data resources but to the customer as well.

Views can be constructed to show a view of data that is different from what physically exists in the underlying base tables. Specific columns can be shown while other columns are hidden. This helps prevent sensitive information such as salary, medical, or credit card data from getting into the wrong hands. Or a view can contain a WHERE clause with any degree of complexity to restrict what rows appear for a group of users while hiding other rows. In the next example, a view called SOFTWARE_PRODUCTS_VIEW is created that displays all columns from the original table except the product cost (PRODCOST) column, and restricts all rows except “Software” from the PRODUCTS table.

## SQL Code

```
PROC SQL;
    CREATE VIEW SOFTWARE_PRODUCTS_VIEW AS
        SELECT prodnum, prodname, manunum, prodtype
            FROM PRODUCTS
                WHERE UPCASE(PRODTYPE) IN ('SOFTWARE');
QUIT;
```

## SAS Log Results

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

## SQL Code

```
PROC SQL;
SELECT *
FROM SOFTWARE_PRODUCTS_VIEW
ORDER BY prodname;
QUIT;
```

## Results

| Product Number | Product Name | Manufacturer Number | Product Type |
|---|---|---|---|
| 5002 | Database Software | 500 | Software |
| 5004 | Graphics Software | 500 | Software |
| 5001 | Spreadsheet Software | 500 | Software |
| 5003 | Wordprocessor Software | 500 | Software |

## Hiding Logic Complexities

Because complex logic constructs such as multi-way table joins, subqueries, or hard-to-understand data relationships might be beyond the skill of other staff in your area, you might want to build or customize views so that others can access the information easily. The next example illustrates how
