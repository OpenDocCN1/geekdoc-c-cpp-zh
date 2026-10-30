The SELECT statement is always used with a FROM clause. The FROM clause identifies the table(s) that make up the source for the data.

Try this: Start a new query in Design view. Close the Show Table dialog box (if it's open), select the Design tab on the Ribbon, and choose View ▸ SQL View. In SQL view, type in the SELECT statement shown in Figure 14.3, and then run the query by selecting Run on the Design tab of the Ribbon.

# FIGURE 14.3

A basic SELECT statement in SQL view.

![](bbox=[0.22, 0.44, 0.48, 0.55])

Congratulations! You've just written your first query manually.

# NOTE

You may notice that the SQL statement automatically created by Access in Figure 14.2 has a semicolon at the end of it. The semicolon is a standard way to end a SQL statement and is required by some database programs. However, it isn't necessary to end your SQL statements with a semicolon in Access, because Access will automatically add it when the query compiles.

# Selecting specific columns

You can retrieve specific columns from your data set by explicitly defining the columns in your SELECT statement, as follows:

```
SELECT AccountManagerID, FullName, [Email Address]
FROM Dim_AccountManagers
```

# CAUTION

Any column in your database with a name that includes spaces or a non-alphanumeric character must be enclosed within brackets ([]) in your SQL statement. For example, the SQL statement selecting data from a column called Email Address would be referred to as [Email Address].

# Selecting all columns

Using the wildcard (*) allows you to select all columns from a data set without having to define every column explicitly:

```
SELECT * FROM Dim_AccountManagers
```