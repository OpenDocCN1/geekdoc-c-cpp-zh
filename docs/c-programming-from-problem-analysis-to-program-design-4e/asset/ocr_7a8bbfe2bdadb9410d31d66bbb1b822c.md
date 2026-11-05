**NOTE** A **primary key** is a column (field) or combination of columns that uniquely identifies a row in a table. A **foreign key** is a column that refers to a column in another table. The foreign key is used to link the two tables.

You selectively choose the columns you want returned from both tables. It is not necessary to return the key that is used to link the tables. However, many applications benefit from retrieving the key columns for later use. For this example, two columns are returned from the memberTable (FirstName and LastName) and one is returned from the departmentTable (major_Name).

SQL statements can also be written to create tables or to insert, delete, and update data in a table. When you are working with ADO.NET, it is extremely helpful to be able to write SQL statements. To insert values into a table, use the SQL INSERT INTO clause followed by the table name and the columns for which you have values. The VALUES keyword is used with a parenthesized list of new values, as shown in Example 14–7.

# EXAMPLE 14.7

```
```sql
INSERT INTO memberTable(StudentID, FirstName, LastName, PhoneNumber)
VALUES (1123, 'Kathy', 'Weizel', 2345678);
```
```

The SQL DELETE keyword is used to remove rows from a table. To identify which rows to delete, use the FROM and WHERE clauses. Example 14–8 illustrates removing the last record from the table shown in Figure 14–1.

# EXAMPLE 14.8

```
```sql
DELETE FROM memberTable
WHERE (StudentID = 1299);
```
```

The final example illustrates writing a SQL UPDATE statement. The SET and WHERE clauses are normally used to identify which row and values to change. Referring back to Figure 14–1, to change Rachel Smith’s last name to Hakim, you could write an UPDATE SQL statement, as shown in Example 14–9.

# EXAMPLE 14.9

```
```sql
UPDATE memberTable
SET LastName = 'Hakim'
WHERE (StudentID = 1234);
```
```