that the database field identifiers do not have spaces as part of the name. If a database table's field has a space, the field name would have to be enclosed in square brackets, as in [Phone Number], for the SQL statement.

The general format for the WHERE clause is as follows:

```
WHERE columnName = value
```

Compound expressions can be combined with AND, OR, or NOT. Relational operators can also be used with WHERE clauses, including >, <, >=, <=, and a single equal symbol used for equality. To test for "not equal to," <> is used. To write conditional expressions that test to determine if a value falls within a specified range, the keyword BETWEEN can be inserted before the first value. The compound expression AND is used between the two values. To use a date as the value, the date value is enclosed in the # symbol for Microsoft Access. As noted previously, database management systems use slightly different dialects. Microsoft SQL Server uses single apostrophes as date delimiters instead of the # symbol, as follows:

```
WHERE (aDate BETWEEN #10/12/2012# AND #10/12/2013#)--Access
WHERE (aDate BETWEEN '10/12/2012' AND '10/12/2013')--SQL Server
```

In addition to selecting data for viewing using a single table, you can use the SELECT statement to retrieve results from multiple tables by joining them using a common field. One way to combine tables is to use the SQL JOIN clause. The JOIN query combines columns of one table to columns of another to create a single table, matching up a column from one table to a column in the other table. The JOIN query does not alter either table, but temporarily combines data from each table to be viewed as a single table. One type of JOIN statement is an INNER JOIN.

The INNER JOIN used with a SELECT statement returns all rows from both tables where there is a match. If there are rows in one table that do not have matches in the other table, these rows are not returned. To use the JOIN clause, identify the columns from both tables that should be returned. Their names are qualified with a prefixing dot and the table name. Instead of using a WHERE clause to identify the rows to be returned, the keyword INNER JOIN and ON are used with the two tables. Suppose a second table named departmentTable had columns of major_ID, major_Name, and major_Chair; an example illustrating how the two tables could be joined is shown in Example 14-6.

# EXAMPLE 14.6

```
SELECT memberTable.FirstName, memberTable.LastName,
departmentTable.major_Name
FROM memberTable INNER JOIN departmentTable ON
memberTable.major_ID = departmentTable.major_ID;
```

Normally, the columns that are used for the join are the primary and/or foreign keys in the two tables. Thus, major_ID would need to appear in both tables. It would serve as a foreign key in the memberTable table. In Example 14-6, the primary key for the department is major_ID. Having common fields in both tables allows the two tables to be linked.