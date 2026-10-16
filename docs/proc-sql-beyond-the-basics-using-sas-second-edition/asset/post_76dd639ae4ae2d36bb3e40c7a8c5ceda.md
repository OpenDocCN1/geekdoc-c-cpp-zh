
## Table 9.1: Debugging Process Steps and Tasks

| Debugging Step | Task Description |
|---|---|
| Problem Identification | 1. Determine if a bug exists in the code. <br>2. Determine what the problem is by playing detective. <br>3. Describe why the problem is a bug. <br>4. Determine what the code should do. <br>5. Determine what the code is doing. |
| Information Collection | 1. Collect user comments and feedback. <br>6. Collect personal observations and symptoms. <br>7. Review SAS log information. <br>8. Collect test case(s) that highlight the problem. <br>9. Capture environmental information (for example, system settings, operating environment, external elements, etc.). |
| Problem Assessment & Classification | 1. Develop a theory about what caused the problem. <br>10. Review the code. <br>11. Classify the problem into one of the following categories: <br>- Requirements problem <br>- Syntax error <br>- CPU problem <br>- Memory problem <br>- Storage problem <br>- I/O problem <br>- Logic problem |
| Problem Resolution | 1. Propose a solution. <br>12. Describe why the solution will fix the problem. <br>13. Verify that the solution will not cause additional problems. <br>14. Fix the problem by implementing the solution. |
| Validate Solution | 1. Verify whether the problem still exists. <br>15. Verify whether the problem can be recreated or reproduced. <br>16. Determine whether other methods can cause the same problem to occur. <br>17. Verify that the solution does not cause other problems. |

## Types of Problems

The leading causes of SQL programming problems include misusing the language syntax; referencing data, especially column data, incorrectly; ignoring or incorrectly specifying system parameters; and constructing syntactically correct but illogical code that does not produce results as expected.

Usage errors can cause SAS to stop processing, produce warnings, or produce unexpected results. Table 9.2 illustrates the four types of usage errors and briefly describes each.

## Table 9.2: Types of Usage Errors

| Problem | Description |
|---|---|
| Syntax | Syntax problems are a result of one or more violations of the SQL procedure language constructs. These problems can prevent a program from processing until you make the required changes. For example, a variable that is referenced in a SELECT statement but is not found in the referenced table causes the program to stop. |
| Data | Data problems are a result of an inconsistency between the data and the program specification. These problems can prevent a program from processing, but might allow processing to continue and result in the assignment of missing, incomplete, or unreliable data. For example, missing values might be generated in a column when character data is incorrectly referenced as numeric data. |
| System-related | System-related problems frequently result from specifying incompatible system options or choosing the wrong system option values. These problems can prevent a program from processing, but most frequently permit processing to occur with unsatisfactory results. For example, forgetting to specify a title statement has little effect on the production of output, but it might force the program to be rerun after the addition of one or more titles. |
| Logic | Logic problems are frequently the result of not specifying a coding condition correctly. For example, specifying an OR condition when an AND condition is needed might produce wrong results without any warnings, errors, or notes. |

Other sources of problems can occur in a program for a variety of reasons. Table 9.3 illustrates these other problem sources and briefly describes each.

## Table 9.3: Other Types of Errors

| Problem | Description |
|---|---|
| Feature Creep | Additional features can creep into a program or application during the design, implementation, or testing phases. This can create a greater likelihood of problems. |
| Solution Complexity | More complex or esoteric solutions can also translate into problems. Difficult-to-maintain programs can result. |
| Requirements | Requirements might be inadequately stated, misunderstood, or omitted. In these situations, programs might not meet the needs of the user community and be classified as bugs. |
| Testing Environment | Inadequate testing environments, poor test plans, or insufficient test time often lead to bug-filled programs. In these situations, bugs can slip through the testing phase and into the production environment. |

## Troubleshooting and Debugging Techniques

PROC SQL provides numerous troubleshooting and debugging capabilities for the practitioner to choose from. From statements to options to macro variables, you can use the various techniques to control the process of finding and gathering information about SQL procedure coding problems quickly and easily.

## Validating Queries with the VALIDATE Statement

The SQL procedure syntax checker identifies syntax errors before any data is processed. Syntax checking is automatically turned on in the SQL procedure without any statements or options being specified. But to enable syntax checking without automatically executing a step, you can specify a VALIDATE statement at the beginning of a SELECT statement or, as will be presented later, specify the NOEXEC option.

The VALIDATE statement is available for SAS users to control what SELECT statement is checked. Because you specify a VALIDATE statement before a SELECT statement, you are better able to control the process of debugging code. A message that indicates syntax correctness is automatically displayed in the SAS log when code syntax is valid. Otherwise, an error message is displayed that identifies the coding violation. In the next example, a VALIDATE statement is specified at the beginning of a SELECT statement to enable syntax checking without code execution. The SAS log shows that the code contains valid syntax and automatically displays a message to that effect.

## SQL Code

```
PROC SQL;
    VALIDATE
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
QUIT;
```

## SAS Log Results

```
PROC SQL;
    VALIDATE
        SELECT *
            FROM PRODUCTS
                WHERE PRODTYPE = 'Software';
NOTE: PROC SQL statement has valid syntax.
QUIT;
```

## Documented PROC SQL Options and Statement

This section illustrates examples of widely used and documented troubleshooting and debugging SQL options along with the RESET statement. A description and a working example of each option and statement are presented below.

## FEEDBACK/NOFEEDBACK Option

The FEEDBACK option displays additional documentation with SELECT queries. When specified, this option expands a SELECT * (wildcard) statement into a list of columns that it represents by displaying the names of each column in the underlying table(s) as well as any resolved macro values and macro variables. The column display order of a SELECT * statement is determined by the order defined in the table’s record descriptor.

The following example illustrates the FEEDBACK option. Because a SELECT * statement does not automatically display the columns it represents, it might be important to expand the individual column names by specifying the FEEDBACK option. This becomes particularly useful for determining whether a desired column is present in the output and available for documentation purposes. The results of the expanded list of columns are displayed in the SAS log.

## SQL Code

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS;
QUIT;
```

## SAS Log Results

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS;
NOTE: Statement transforms to:
    select PRODUCTS.prodnum, PRODUCTS.prodname, PRODUCTS.manunum,
            PRODUCTS.prodtype, PRODUCTS.prodcost
        from WORK.PRODUCTS;
QUIT;
```

The FEEDBACK option can be particularly helpful in determining the column order when joining two or more tables. The next example illustrates the expansion of the columns in the SELECT * statement in a two-way equijoin. The FEEDBACK option displays all the columns in both tables.

## SQL Code

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS, MANUFACTURERS
            WHERE PRODUCTS.MANUNUM = MANUFACTURERS.MANUNUM AND
                  MANUFACTURERS.MANUNAME = 'KPL Enterprises';
QUIT;
```

## SAS Log Results

```
PROC SQL FEEDBACK;
    SELECT *
        FROM PRODUCTS, MANUFACTURERS
            WHERE PRODUCTS.MANUNUM = MANUFACTURERS.MANUNUM AND
                  MANUFACTURERS.MANUNAME = 'KPL Enterprises';
NOTE: Statement transforms to:
    select PRODUCTS.prodnum, PRODUCTS.prodname, PRODUCTS.manunum,
            PRODUCTS.prodtype, PRODUCTS.prodcost, MANUFACTURERS.manunum,
            MANUFACTURERS.manuname, MANUFACTURERS.manucity,
            MANUFACTURERS.manustat
        from PRODUCTS, MANUFACTURERS
        where (PRODUCTS.manunum=MANUFACTURERS.manunum) and
              (MANUFACTURERS.manuname='KPL Enterprises');
QUIT;
```

The FEEDBACK option can also be used to display macro value and macro variable resolution. The next example shows the macro resolution of the macro variables &LIB, &TABLE, and &GROUPBY for debugging purposes.
