# Introduction

Expressions in the SQL procedure can be simple or complex and are represented by a combination of columns, symbols, operators, functions, constants, and literals. Specified in SQL statements and clauses, expressions are typically used in conditional logic constructs to test or compare a value against another value. The application of an expression in a CASE expression allows individual rows of data to be processed and grouped using one or more expressions. In particular, data can be recoded and reshaped to expand the data analysis and processing perspective.

# Conditional Logic

As experienced PROC SQL programmers know, it is often necessary to test and evaluate conditions as true or false. From a programming perspective, the evaluation of a condition determines which of the alternate paths a program will follow. Conditional logic in the SQL procedure is frequently implemented in a WHERE clause to reference constants and relationships among columns and values. The SQL procedure also allows the identification and assignment of data values in a SELECT statement using case-expressions (which are described in the next section). To show how constants and relationships are referenced in a WHERE clause, a simple example is illustrated.

The next example shows a WHERE clause subsetting products from the PRODUCTS table that cost less than $400.00. During execution, the expression evaluates to true when the value of PRODCOST is less than $400.00. Otherwise, when the value of PRODCOST is greater than or equal to $400.00, the expression evaluates to false. This is an important concept because data rows are only selected when the WHERE clause expression evaluates to true.

# SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
        WHERE PRODCOST < 400.00;
QUIT;
```

In the next example, the following relation evaluates whether the cost of a product (PRODCOST) is greater than $400.00. When the WHERE clause expression evaluates to true, which means that PRODCOST is greater than $400.00, then the rows of data are selected. Otherwise, when the value is less than or equal to $400.00, the expression evaluates to false.

# SQL Code

```
PROC SQL;
    SELECT *
        FROM PRODUCTS
        WHERE PRODCOST > 400.00;
QUIT;
```