
## Results

|  | A | B | C | D | E |
|---|---|---|---|---|---|
| 1 | Product Number | Product Name | Manufacturer Number | Product Type | Product Cost |
| 2 |  |  |  |  | |
| 3 |  | 1110 Dream Machine | 111 | Workstation | $3,200.00 |
| 4 |  | 1200 Business Machine | 120 | Workstation | $3,300.00 |
| 5 |  | 1700 Travel Laptop | 170 | Laptop | $3,400.00 |
| 6 |  | 2101 Analog Cell Phone | 210 | Phone | $35.00 |
| 7 |  | 2102 Digital Cell Phone | 210 | Phone | $175.00 |
| 8 |  | 2200 Office Phone | 220 | Phone | $130.00 |
| 9 |  | 5001 Spreadsheet Software | 500 | Software | $299.00 |
| 10 |  | 5002 Database Software | 500 | Software | $399.00 |
| 11 |  | 5003 Wordprocessor Software | 500 | Software | $299.00 |
| 12 |  | 5004 Graphics Software | 500 | Software | $299.00 |

## Delivering Results to the Web

With the popularity of the Internet, you may find it useful to deploy selected pieces of output on your intranet or website. ODS makes deploying output to the web a snap. The HTML destination creates syntactically correct HTML code to be used with one of the leading Internet browsers.

Four types of files can be produced with the ODS HTML destination:

- body
- contents
- page
- frame

A unique file name must be assigned to each file that is created with the ODS HTML statement. A custom and integrated file structure is automatically created when each file is combined with a frame file. To improve navigation and access of information, the web browser automatically places horizontal and vertical scroll bars on the generated page if necessary.

The next example illustrates PROC SQL output being sent to external HTML files using the HTML format engine. First, the default Listing destination is closed, and then the HTML format engine is opened specifying BODY, CONTENTS, PAGE, and FRAME external files for the routing of SQL procedure results. After the SQL procedure executes, the HTML destination is closed and the default Listing destination is opened.

## SQL Code

```
ODS LISTING CLOSE;
ODS HTML
    BODY='Products-body.html'
    CONTENTS='Products-contents.html'
    PAGE='Products-page.html'
```

```
FRAME='Products-frame.html';

PROC SQL;
    TITLE1 'Products List';
    SELECT prodname, prodtype, prodcost, prodnum
    FROM PRODUCTS
        ORDER BY prodtype;
QUIT;

ODS HTML CLOSE;
ODS LISTING;
```

## Results

![](img/9d3e4d8fa063e50a0c9985e34cf9d6e8_141_0.png)

## Summary

- 1. A blank line can be displayed between each row of output (see the “Writing a Blank Line between Each Row” section).
- 2. Columns can be concatenated to form a single column of data (see the “Concatenating Character Strings” section).
- 3. Text and constants can be inserted between selected columns (see the “Inserting Text and Constants between Columns” section).
- 4. Numeric or character scalar values can be produced with expressions (see the “Using Scalar Expressions with Selected Columns” section).
- 5. User-defined values can be assigned to derived column headers (see the “Using Scalar Expressions with Selected Columns” section).
- 6. Formats can be assigned and stored permanently to automatically display a user-defined formatted value instead of the unformatted value (see the “Using Scalar Expressions with Selected Columns” section).

## Introduction

Expressions in the SQL procedure can be simple or complex and are represented by a combination of columns, symbols, operators, functions, constants, and literals. Specified in SQL statements and clauses, expressions are typically used in conditional logic constructs to test or compare a value against another value. The application of an expression in a CASE expression allows individual rows of data to be processed and grouped using one or more expressions. In particular, data can be recoded and reshaped to expand the data analysis and processing perspective.

## Conditional Logic

As experienced PROC SQL programmers know, it is often necessary to test and evaluate conditions as true or false. From a programming perspective, the evaluation of a condition determines which of the alternate paths a program will follow. Conditional logic in the SQL procedure is frequently implemented in a WHERE clause to reference constants and relationships among columns and values. The SQL procedure also allows the identification and assignment of data values in a SELECT statement using case-expressions (which are described in the next section). To show how constants and relationships are referenced in a WHERE clause, a simple example is illustrated.

The next example shows a WHERE clause subsetting products from the PRODUCTS table that cost less than $400.00. During execution, the expression evaluates to true when the value of PRODCOST is less than $400.00. Otherwise, when the value of PRODCOST is greater than or equal to $400.00, the expression evaluates to false. This is an important concept because data rows are only selected when the WHERE clause expression evaluates to true.

## SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
        WHERE PRODCOST < 400.00;
QUIT;
```

In the next example, the following relation evaluates whether the cost of a product (PRODCOST) is greater than $400.00. When the WHERE clause expression evaluates to true, which means that PRODCOST is greater than $400.00, then the rows of data are selected. Otherwise, when the value is less than or equal to $400.00, the expression evaluates to false.

## SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
        WHERE PRODCOST > 400.00;
QUIT;
```

A relation can also be used with nonnumeric literals and nonnumeric columns. In the next example, a case-sensitive expression is constructed to represent the type of product (PRODTYPE) made by a manufacturer. When evaluated, a condition of true or false is produced depending on whether the current value of PRODTYPE is identical (character-by- character) to the literal value “Software”. When a condition of true occurs, then the rows of data satisfying the expression are selected; otherwise, they are not selected.

## SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE PRODTYPE = "Software";
QUIT;
```

To ensure a character-by-character match of a character value, the previous expression could be specified with the UPCASE function as follows.

## SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
            WHERE UPCASE(PRODTYPE) = "SOFTWARE";
QUIT;
```

When the relations < and > are defined for nonnumeric values, the issue of implementation-dependent collating sequence for characters comes into play. For example, “A” < “B” is true, “Y” < “Z” is “true”, “B” < “A” is “false”, and so on. For more information about character collating sequences, refer to your specific operating system documentation.

## CASE Expressions

In the SQL procedure, a CASE expression provides a way of determining what the resulting value will be from all the rows in a table (or view). Similar to a DATA step SELECT statement (or IF-THEN/ELSE statement), a CASE expression is based on some condition and the condition uses a WHEN-THEN clause to determine what the resulting value will be. An optional ELSE expression can be specified to handle an alternative action if none of the expression(s) identified in the WHEN condition(s) is satisfied.

The SQL procedure supports two forms of CASE expressions: simple and searched. CASE expressions can be specified in a SELECT clause, a WHERE clause, an ORDER BY clause, a HAVING clause, a join construct, and anywhere an expression can be used. A CASE expression must be a valid PROC SQL expression and conform to syntax rules similar to DATA step SELECT-WHEN statements. Before specific CASE expression examples are shown, it’s important to illustrate the basic syntax, which is shown below.

```
CASE <column-name>
    WHEN when-condition THEN result-expression
    <WHEN when-condition THEN result-expression> ...
    <ELSE result-expression>
END
```

The CASE syntax contains everything from CASE to END. A column-name can optionally be specified as part of the CASE expression. If present, it is automatically made available to each WHEN condition. When it is not specified, the column name must be coded in each WHEN condition. Let’s examine how a CASE expression works.

One or more WHEN conditions can be specified in a CASE expression and are evaluated in the order listed. If a WHEN condition is satisfied by a row in a table (or view), then it is considered “true” and the result expression following the THEN keyword is processed. The remaining WHEN conditions in the CASE expression are skipped. If a WHEN condition is “false,” the next WHEN condition is evaluated. SQL evaluates each WHEN condition until a “true” condition is found. Or, in the event that all WHEN conditions are “false,” it then executes the ELSE expression and assigns its value to the CASE expression’s result. A missing value is assigned to a CASE expression when an ELSE expression is not specified and each WHEN condition is “false.”

## Simple Case Expression

As its name implies, a simple CASE expression provides a useful way to perform the simplest type of comparisons. The syntax requires a column name from an underlying table to be specified as part of the CASE expression. This not only eliminates having to continually repeat the column name in each WHEN condition, it also reduces the number of keystrokes, making the code easier to read (and support). Simple CASE expressions possess the following features:

- Allows only equality checks.
- Evaluates the specified WHEN conditions in the order specified.
- Evaluates the input-expression for each WHEN condition.
- Returns the result-expression of the first input-expression that evaluates to “true.”
- If no input-expressions evaluate to “true,” then the ELSE condition is processed.
- When an ELSE condition isn’t specified, a NULL value is assigned.

## Simple CASE Expression in a SELECT Clause

To best show how a simple CASE expression works, an example in a SELECT clause is illustrated. The objective calls for the value assignment of “East” to manufacturers in Florida, “Central” to manufacturers in Texas, “West” to manufacturers in California, or “Unknown” to manufacturers not residing in Florida, Texas, and California. The manufacturer’s state of residence (MANUSTAT) column is specified in the CASE expression along with its associated WHEN conditions with assigned values. Finally, a column heading of Region is assigned to the derived output column using the AS keyword.
