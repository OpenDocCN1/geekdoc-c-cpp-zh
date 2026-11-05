columns of `major_ID`, `major_Name`, and `major_Chair`; an example illustrating how the two tables could be joined is shown in Example 14–6.

# Example 14-6

```
SELECT memberTable.FirstName, memberTable.LastName,
       departmentTable.major_Name
FROM memberTable INNER JOIN departmentTable ON
     memberTable.major_ID = departmentTable.major_ID;
```

Normally, the columns that are used for the join are the primary and/or foreign keys in the two tables. Thus, `major_ID` would need to appear in both tables. It would serve as a foreign key in the `memberTable`. In Example 14–6, the primary key for the department is `major_ID`. Having common fields in both tables allows the two tables to be linked.

A **primary key** is a column (field) or combination of columns that uniquely identifies a row in a table. A **foreign key** is a column that refers to a column in another table. The foreign key is used to link the two tables.

You selectively choose the columns you want returned from both tables. It is not necessary to return the key that is used to link the tables. However, many applications benefit from retrieving the key columns for later use. For this example, two columns are returned from the `memberTable` (`FirstName` and `LastName`) and one is returned from the `departmentTable` (`major_Name`).

SQL statements can also be written to create tables or to insert, delete, and update data in a table. When you are working with ADO.NET, it is extremely helpful to be able to write SQL statements. To insert values into a table, use the SQL `INSERT INTO` clause followed by the table name and the columns for which you have values. The `VALUES` keyword is used with a parenthesized list of new values, as shown in Example 14–7.

# Example 14-7

```
INSERT INTO memberTable(StudentID, FirstName, LastName, PhoneNumber)
VALUES (11234, 'Kathy', 'Weizel', 2345678);
```

The SQL `DELETE` keyword is used to remove rows from a table. To identify which rows to delete, use the `FROM` and `WHERE` clauses. Example 14–8 illustrates removing the first record from the table shown in Figure 14–1.