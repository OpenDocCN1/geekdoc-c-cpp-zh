
![](img/844f608d10a44654833ea5efc8a2e7a7_647_0.png)

## The tables that make up the MMABooks database

## Description
- The Customers table contains a row for each customer. Its primary key is CustomerID, an identity column that’s generated automatically when a new customer is created. State is a foreign key that relates each customer to a row in the States table.
- The Invoices table contains a row for each invoice. Its primary key is InvoiceID, an identity column that’s generated automatically when a new invoice is created. CustomerID is a foreign key that relates each invoice to a customer.
- The InvoiceLineItems table contains one row for each line item of each invoice. Its primary key is a combination of InvoiceID and ProductCode. InvoiceID is a foreign key that relates each line item to an invoice, and ProductCode is a foreign key that relates each line item to a product.
- The Products table contains a row for each product. Its primary key is ProductCode, a 10-character code that identifies each product.
- The States table contains a row for each state. Its primary key is StateCode.
- The OrderOptions table contains a single row that stores the sales tax and shipping charges used by the application. Its primary key is OptionID.
- The relationships between the tables in this diagram appear as links, where the endpoints indicate the type of relationship. A key indicates the “one” side of a relationship, and the infinity symbol (∞) indicates the “many” side.

## How to use SQL to work with a relational database

In the topics that follow, you’ll learn about the four SQL statements that you can use to manipulate the data in a database: SELECT, INSERT, UPDATE, and DELETE. To master the material in this book, you need to understand what these statements do and how they’re coded.

Although you’ll learn the basics of coding these statements in the topics that follow, you may want to know more than what’s presented here. In that case, we recommend our book, Murach’s SQL Server for Developers. In addition to the SELECT, INSERT, UPDATE, and DELETE statements, this book teaches you how to code the statements that you use to define the data in a database, and it teaches you how to use other features of SQL Server that the top professionals use.

Although SQL is a standard language, each DBMS is likely to have its own SQL dialect, which includes extensions to the standard language. So when you use SQL, you need to make sure you’re using the dialect that’s supported by your DBMS. In this chapter and throughout this book, all of the SQL examples are for Microsoft SQL Server’s dialect, which is called Transact-SQL.

## How to query a single table

Figure 19-7 shows how to use a SELECT statement to query a single table in a database. In the syntax summary at the top of this figure, you can see that the SELECT clause names the columns to be retrieved and the FROM clause names the table that contains the columns. You can also code a WHERE clause that gives criteria for the rows to be selected. And you can code an ORDER BY clause that names one or more columns that the results should be sorted by and indicates whether each column should be sorted in ascending or descending sequence.

If you study the SELECT statement below the syntax summary, you can see how this works. Here, the SELECT statement retrieves two columns from the Customers table for all customers who live in the state of Washington. It sorts the returned rows by the Name column.

This figure also shows the result table, or result set, that’s returned by the SELECT statement. A result set is a logical table that’s created temporarily within the database. When an application requests data from a database, it receives a result set.

### Simplified syntax of the SELECT statement

```
SELECT column-1 [, column-2]...
FROM table-1
[WHERE selection-criteria]
[ORDER BY column-1 [ASC|DESC] [, column-2 [ASC|DESC]]...]
```

### A SELECT statement that retrieves and sorts selected columns and rows from the Customers table

```
SELECT Name, City
FROM Customers
WHERE State = 'WA'
ORDER BY Name
```

### The result set defined by the SELECT statement

| # | Name | City |
| - | ---- | ---- |
| 1 | Allen, Craig | Pullman |
| 2 | Antalcy, S. | Seattle |
| 3 | Cassara, Glenn | Van |
| 4 | Giraka, Eric | Seattle |
| 5 | Hester, Maurice | Kennewick |
| 6 | Howell, Kim | Renton |
| 7 | McMillen, G | Kirkland |
| 8 | Millard, Dwayne | Seattle |
| 9 | Oneil, Ri | Olympia |
| 10 | Seaver, Glenda | Mountlake Terrace |
| 11 | Smith, Lloyd | Pullman |
| 12 | Sundaram, Kelly | Oregon |

### Concepts
- The result of a SELECT statement is a result table, or result set, like the one shown above. A result set is a logical set of rows that consists of all of the columns and rows requested by the SELECT statement.
- The SELECT clause lists the columns to be included in the result set. This list can include calculated columns that are calculated from other columns.
- The FROM clause names the table the data will be retrieved from.
- The WHERE clause provides a condition that specifies which rows should be retrieved. To retrieve all rows from a table, omit the WHERE clause.
- The ORDER BY clause lists the columns that the results are sorted by and indicates whether each column is sorted in ascending or descending sequence.
- To select all of the columns in a table, you can code an asterisk (*) in place of the column names. For example, this statement will select all of the columns from the Customers table:

```
SELECT * FROM Customers
```

> Figure 19-7 How to query a single table

## How to join data from two or more tables

Figure 19-8 presents the syntax of the SELECT statement for retrieving data from two tables. This type of operation is called a *join* because the data from the two tables is joined together into a single result set. For example, the SELECT statement in this figure joins data from the InvoiceLineItems and Products tables into a single result set.

An *inner join* is the most common type of join. When you use an inner join, rows from the two tables in the join are included in the result set only if their related columns match. These matching columns are specified in the FROM clause of the SELECT statement. In the first SELECT statement in this figure, for example, rows from the InvoiceLineItems and Products tables are included only if the value of the ProductCode column in the Products table matches the value of the ProductCode column in one or more rows in the InvoiceLineItems table.

Notice that each column in the SELECT clause is qualified to indicate which table the column is to be retrieved from. For example, the InvoiceID, ProductCode, UnitPrice, and Quantity columns are retrieved from the InvoiceLineItems table, but the Description column comes from the Products table. Qualification is only required for columns that exist in both tables. In this case, only the ProductCode column requires qualification because both the InvoiceLineItems and the Products tables have a column named ProductCode. However, we recommend that you qualify all of the columns just to make it clear which table each column is being retrieved from.

One way to make it easier to qualify your columns is to use *aliases* for your table names. To do that, you code the AS keyword after the table name, followed by the alias. Note that you can omit the AS keyword and just code the alias, but including the AS keyword makes your code more clear.

In the second SELECT statement in this figure, the first SELECT statement is re-written to use an alias of ‘li’ for the InvoiceLineItems table and an alias of ‘p’ for the Products table. Then, these aliases are used instead of the full table names to qualify the columns. As you can see, this makes the SQL shorter and easier to read.

Although this figure shows how to join data from two tables, you should know that you can extend this syntax to join data from additional tables. If, for example, you want to include data from the Invoices table along with the InvoiceLineItems and Products data, you could code a FROM clause like this:

```
FROM Invoices AS i
    INNER JOIN InvoiceLineItems AS li
    ON i.InvoiceID = li.InvoiceID
    INNER JOIN Products AS p
    ON li.ProductCode = p.ProductCode
```

Then, in the column list of the SELECT statement, you can include any of the columns in the Invoices, InvoiceLineItems, and Products tables.
