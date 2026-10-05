
# Chapter 17 An introduction to database programming 521

## The tables that make up the MMBooks database

| Customers | Invoices |
| :--- | :--- |
| CustomerID | InvoiceID |
| Name | CustomerID |
| Address | InvoiceDate |
| City | ProductTotal |
| State | SalesTax |
| ZipCode | Shipping |
| | InvoiceTotal |
| States | InvoiceLineItems |
| StateCode | InvoiceID |
| StateName | ProductCode |
| | UnitPrice |
| | Quantity |
| OrderOptions | ItemTotal |
| SalesTax | |
| FirstBookShipCharge | ProductCode |
| AdditionalBookShipC | Description |
| UnitPrice | |
| OnHandQuantity | |

### Description

The Customers table contains a row for each customer. Its primary key is CustomerID, an identity column that is generated automatically when a new customer is created. State is a foreign key that relates each customer to a row in the States table.
- The Invoices table contains a row for each invoice. Its primary key is InvoiceID, an identity column that is generated automatically when a new invoice is created. CustomerID is a foreign key that relates each invoice to a customer.
- The InvoiceLineItems table contains one row for each line item of invoice. Its primary key is a combination of InvoiceID and ProductCode. InvoiceID is a foreign key that relates each line item to an invoice, and ProductCode is a foreign key that relates each line to a product.
- The Products table contains a row for each product. Its primary key is ProductCode, a 10-character code identifies each product.
- The States table contains a row for each state. Its primary key is StateCode.
- The OrderOptions table contains a single row for state that stores the sales tax and shipping charges used by the application.
- The relationships between the tables in this diagram appear as links, where the endpoints indicate the type of relationship. A key indicates the “one” side of a relationship, and the infinity symbol (∞) indicates the “many” side.

Figure 17-6 The design of the MMBooks database

## How to use SQL to work with relational database

In the topics that follow, you'll learn about the four SQL statements that you can use to manipulate the data in a database: Select, Insert, Update, and Delete. To master the material in this book, you need to understand what these statements do and how they’re re-coded.

Although you'll learn the basics of coding these statements in the topics that follow, you may want to know more than what's presented here. In that case, we recommend our book, Murach's SQL Server 2008 for Developers. In addition to the Select, Insert, Update, and Delete statements, this book teaches you how to code the statements that you use to define the data in a database, and it teaches you how to use other features of SQL Server that the professionals use.

Although SQL is a standard language, each DBMS is likely to have its own SQL dialect, which includes extensions to the standard language. So when you use SQL, you need to make sure that you're using the dialect that's supported by your DBMS. In this chapter and throughout this book, all of the SQL examples are for Microsoft SQL Server's dialect, which is called Transact-SQL.

## How to query a single table

Figure 17-7 shows how to use a Select statement to query a single table in a database. In the syntax summary at the top of this figure, you can see that the Select clause names the columns to be retrieved and the From clause names the table that contains the columns. You can also code a Where clause that gives criteria for the rows to be selected. And you can code an Order By clause that names one or more columns that the results should be sorted by indicates whether each column should be sorted in ascending or descending sequence.

If you study the Select statement below the syntax summary, you can see how this works. Here, the Select statement retrieves two columns from the Customers table for all customers who live in the state of Washington. It sorts the returned rows by the Name column.

This figure also shows the result table, or result set, that's returned by the Select statement. A result set is a logical table that's created temporarily within the database. When an application requests data from a database, it receives a result set.

# Chapter 17 An introduction to database programming 523

## Simplified syntax of the Select statement

```
Select column-1 [, column-2]...
From table-1
[Where selection-criteria]
[Order By column-1 [Asc] [Desc], column-2 [Asc] [Desc]]...]
```

## A Select statement retrieves and sorts selected columns from the Customers table

```
Select Name, City
From Customers
Where State = 'WA'
Order By Name
```

## The result set defined by the Select statement

| Name | City |
| :--- | :--- |
| Allen, Craig | Pullman |
| Antalocy, S. | Seattle |
| Cassara, Glenn | Van |
| Giraka, Eric | Kennewickrick |
| Hester, Maurice | Seattle |
| Howell, Kim | Renton |
| Mcmillen, G | Kirkland |
| Millard, Dwayne | Seattle |
| Oneil, Ri | Olympia |
| Seaver, Glenda | Mountlake Terr... |
| Smith, Lloyd | Pullman |
| Sundaram, Kelly | Oregon |

## Concepts

- The result of a Select statement is a result table, or result set, like the one shown above.
- A result set is a logical set of rows that contains all of the columns and rows requested.
- The Select clause lists the columns to be included in the result set.
- The From clause names the table the data will be retrieved from.
- The Where clause provides a condition that specifies which rows should be retrieved.
- The Order By clause lists the columns that the results are sorted by and indicates whether each column is in ascending or descending sequence.
- To select all of the columns in a table, you can code an asterisk (*) in place of the column names. For example: `Select * From Customers`

Figure 17-7 How to query a single table

## How to join data from two or more tables

Figure 17-8 presents the syntax of the Select statement for retrieving data from two tables. This type of operation is called a join because the data from the two tables is joined together into a single result set. For example, the Select statement in this figure joins data from the InvoiceLineItems and Products tables into a single result set.

An inner join is the most common type of join. When you use an inner join, rows from the two tables in the join are included in the result set only if the related columns match. These matching columns are specified in the From clause of the Select statement. In the Select statement in this figure, for example, rows from the InvoiceLineItems and Products tables are included only if the value of the ProductCode in Products matches the value of the ProductCode in one or more rows in the InvoiceLineItems table.

Notice that each column in the Select clause is to indicate which table the column is to be retrieved. For example, the InvoiceID, ProductCode, UnitPrice, and Quantity columns are retrieved from the InvoiceLineItems table, but the description column comes from the Products table. Qualification is only required for columns that exist in both tables. In this case, only the ProductCode column requires qualification because both the InvoiceLineItems and the Products tables have a column named ProductCode. However, I recommend that you qualify all of the columns just to make it clear which table each column is retrieved from.

Although this figure shows how to join data from two tables, you should know that you can extend this syntax to join data from additional tables. If, for example, you want to include data from the Invoices table along with the InvoiceLineItems and Products data, you could code a From clause like this:

```
From Invoices
  Join InvoiceLineItems
    On Invoices.InvoiceID = InvoiceLineItems.InvoiceID
  Join Products
    On InvoiceLineItems.ProductCode =
    Products.ProductCode
```

Then, in the column list of the Select statement, you can include any of the columns in the Invoices, InvoiceLineItems, and Products tables.
