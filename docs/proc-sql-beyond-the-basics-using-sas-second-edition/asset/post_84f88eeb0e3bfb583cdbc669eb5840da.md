
## SQL Code
```
PROC SQL LOOPS=8;
    SELECT *
    FROM PRODUCTS;
QUIT;
```

## SAS Log Results
```
PROC SQL LOOPS=8;
    SELECT *
    FROM PRODUCTS;
WARNING: PROC SQL statement interrupted by LOOPS=8 option.
QUIT;
```

## Results

| Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
|---|---|---|---|---|
| 1110 | Dream Machine | 111 | Workstation | $3,200.00 |
| 1200 | Business Machine | 120 | Workstation | $3,300.00 |
| 1700 | Travel Laptop | 170 | Laptop | $3,400.00 |

The next example shows what happens when the LOOPS= option is applied in a three-way join by restricting the number of processed inner loops to 50 to prevent the creation of a large and inefficient internal table. To determine an adequate value to assign to the LOOPS= option, you can specify an &SQLLOOPS macro variable in a %PUT statement. To learn more about this macro variable, see the “Macro Variables” section later in this chapter.

## SQL Code
```
PROC SQL LOOPS=50;
    SELECT P.prodname, P.prodcost,
        M.manuname,
        I.invqty
    FROM PRODUCTS  P,
        MANUFACTURERS  M,
        INVOICE  I
    WHERE P.manunum = M.manunum AND
        P.prodnum = I.prodnum AND
        M.manunum = 500;
QUIT;
```

## Results

| Product Name | Product Cost | Manufacturer Name | Invoice Quantity - Units Sold |
|---|---|---|---|
| Spreadsheet Software | $299.00 | KPL Enterprises | 5 |
| Database Software | $399.00 | KPL Enterprises | 2 |

## RESET Statement

The RESET statement is used to add, drop, or change one or more PROC SQL options without the need to restart the procedure. Once an option is specified, it stays in effect until it is changed or reset. Being able to change options with the RESET statement is a handy debugging technique. The following example illustrates turning off the FEEDBACK option by resetting it to NOFEEDBACK. By turning off this option, you prevent the expansion of a SELECT * (wildcard) statement into a list of columns that it represents.

## SQL Code
```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS;
RESET NOFEEDBACK;
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE='Software';
QUIT;
```

## SAS Log Results
```
SELECT *
    FROM PRODUCTS;
NOTE: Statement transforms to:
select PRODUCTS.prodnum, PRODUCTS.prodname, PRODUCTS.manunum,
    PRODUCTS.prodtype, PRODUCTS.prodcost
    from PRODUCTS;
RESET NOFEEDBACK;
SELECT *
    FROM PRODUCTS
        WHERE PRODTYPE='Software';
```

Multiple options can be reset in a single RESET statement. Options in the PROC SQL and RESET statements can be specified in any order. The next example shows how, in a single RESET statement, double-spaced output is changed to single-spaced output with the NODOUBLE option, row numbers are suppressed with the NONUMBER option, and output rows are changed to the maximum number of rows with the OUTOBS= option.

## SQL Code
```
PROC SQL DOUBLE NUMBER OUTOBS=1;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
RESET NODOUBLE NONUMBER OUTOBS=MAX;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
QUIT;
```

## SAS Log Results
```
PROC SQL DOUBLE NUMBER OUTOBS=1;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
WARNING: Statement terminated early due to OUTOBS=1 option.
RESET NODOUBLE NONUMBER OUTOBS=MAX;
  SELECT *
    FROM PRODUCTS
    WHERE PRODTYPE='Software';
QUIT;
```

## Output Results

| Row | Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
| --- | --- | --- | --- | --- | --- |
| 1 | 5001 | Spreadsheet Software | 500 | Software | $299.00 |

| Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
| --- | --- | --- | --- | --- |
| 5001 | Spreadsheet Software | 500 | Software | $299.00 |
| 5002 | Database Software | 500 | Software | $399.00 |
| 5003 | Wordprocessor Software | 500 | Software | $299.00 |
| 5004 | Graphics Software | 500 | Software | $299.00 |

The next example shows an UPDATE query that reverses any updates that have been performed up to the point of an error using the UNDO_POLICY=REQUIRED (default value) option. (Note: Because this is the default value for this option, it could have been omitted.) A RESET statement

of UNDO_POLICY=NONE is issued before the second update query to change the way updates are handled. The NONE option keeps any updates that have been made regardless of whether an error is detected. A warning message is displayed alerting you to the change in the way updates are handled.

## SQL Code
```
PROC SQL UNDO_POLICY=REQUIRED;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
    RESET UNDO_POLICY=NONE;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
QUIT;
```

## SAS Log Results
```
PROC SQL UNDO_POLICY=REQUIRED;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
NOTE: 1 row was updated in WORK.PRODUCTS.
RESET UNDO_POLICY=NONE;
    UPDATE PRODUCTS
        SET PRODCOST = PRODCOST - (PRODCOST * 0.2)
        WHERE UPCASE(PRODTYPE) = 'LAPTOP';
WARNING: The SQL option UNDO_POLICY=REQUIRED is not in effect. If an error is detected when processing this UPDATE statement, that error will not cause the entire statement to fail.
NOTE: 1 row was updated in WORK.PRODUCTS.
QUIT;
```

## EXEC/NOEXEC Option

The NOEXEC option checks all non-query statements such as CREATE TABLE or ALTER TABLE within the SQL procedure for syntax-related errors and displays any identified errors in the SAS log. The NOEXEC option is similar to the VALIDATE statement in that it checks for syntax correctness without the execution of any input data. The only difference between the NOEXEC option and the VALIDATE statement is in the way they are specified. As was presented earlier, the VALIDATE statement is specified before each SELECT statement; the NOEXEC / EXEC option can be specified as a PROC SQL statement option or in a RESET statement.

To illustrate the troubleshooting and debugging process, the following non-query SQL code will be shown using the NOEXEC and EXEC options. The next example illustrates that the non-query CREATE TABLE statement is not to be executed after its syntax is checked for correctness. As a result of the NOEXEC option being specified, any syntax-related errors are automatically displayed in the SAS log.

## SQL Code
```
PROC SQL NOEXEC;
    CREATE TABLE SOFTWARE_PRODUCTS
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
```

As illustrated on the SAS log, a syntax error is found and the resulting error is displayed.

## SAS Log Results
```
PROC SQL NOEXEC;
    CREATE TABLE SOFTWARE_PRODUCTS
        SELECT *
        ------
            73
ERROR 73-322: Expecting an AS.
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
```

In the next example, with the NOEXEC option still in effect, the AS keyword is specified with the CREATE TABLE statement, which corrects the syntax error that is displayed in the previous example.

## SQL Code
```
CREATE TABLE SOFTWARE_PRODUCTS AS
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE = 'Software';
```

As illustrated in the SAS log, no syntax errors were found, but because the NOEXEC option is still active the CREATE TABLE statement was not executed.

## SAS Log Results
```
PROC SQL NOEXEC;
    CREATE TABLE SOFTWARE_PRODUCTS AS
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
NOTE: Statement not executed due to NOEXEC option.
```

The next example illustrates changing the NOEXEC option to EXEC with a RESET statement, which results in error-free non-query code to execute.

## SQL Code
```
RESET EXEC;
CREATE TABLE SOFTWARE_PRODUCTS  AS
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE = 'Software';
QUIT;
```

As illustrated in the SAS log, no syntax errors were found. And because the RESET statement was specified to change the NOEXEC option to EXEC, the CREATE TABLE statement executed.

## SAS Log Results
```
RESET EXEC;
CREATE TABLE SOFTWARE_PRODUCTS  AS
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE = 'Software';
NOTE: Table WORK.SOFTWARE_PRODUCTS created, with 4 rows and 5 columns.
```

## ERRORSTOP/NOERRORSTOP Option

The ERRORSTOP option instructs SQL to stop executing statements and to continue to check syntax in noninteractive or batch sessions when an error is encountered. Conversely, the NOERRORSTOP option tells SQL to execute statements when an error is encountered and to continue checking syntax. The ERRORSTOP / NOERRORSTOP option can be specified as a PROC SQL statement option or in a RESET statement. The next example illustrates a CREATE TABLE statement being used incorrectly, and shows the SAS log results that are generated when the ERRORSTOP option is specified.

## SQL Code
```
PROC SQL ERRORSTOP;
    CREATE TABLE SOFTWARE_PRODUCTS
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
QUIT;
```

As illustrated in the SAS log, the ERRORSTOP option automatically stops executing the SQL statements and displays a SAS log error message when a syntax error is encountered.
