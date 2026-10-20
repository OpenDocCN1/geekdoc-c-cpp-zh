
## The software components
of a client/server system

Figure 19-2 presents the software components of a typical client/server system. In addition to a *network operating system* that manages the functions of the network, the server requires a *database management system (DBMS)* like Microsoft SQL Server, Oracle, or MySQL. This DBMS manages the databases that are stored on the server.

In contrast to a server, each client requires *application software* to perform useful work. This can be a purchased software package like a financial accounting package, or it can be custom software that’s developed for a specific application. This book, of course, shows you how to use C# for developing custom software for database applications.

Although the application software is run on the client, it uses data that’s stored on the server. To make this communication between the client and the data source possible for a C# application, the client accesses the database via a *data access API* such as Entity Framework Core or ADO.NET.

Once the software for both client and server is installed, the client communicates with the server by passing *SQL queries* (or just *queries*) to the DBMS through the data access API. These queries are written in a standard language called *Structured Query Language (SQL)*. SQL lets any application communicate with any DBMS. After the client sends a query to the DBMS, the DBMS interprets the query and sends the results back to the client. (In conversation, SQL is pronounced as either *S-Q-L* or *sequel.*)

As you can see in this figure, the processing done by a client/server system is divided between the clients and the server. In this case, the DBMS on the server is processing requests made by the application running on the client. Theoretically, at least, this balances the workload between the clients and the server so the system works more efficiently.

## Client software, server software, and the SQL interface

![](img/844f608d10a44654833ea5efc8a2e7a7_639_0.png)

## Server software

- To manage the network, the server runs a network operating system such as Windows Server.
- To store and manage the databases of the client/server system, each server requires a database management system (DBMS) such as Microsoft SQL Server.
- The processing that's done by the DBMS is typically referred to as back-end processing, and the database server is referred to as the back end.

## Client software

- The application software does the work that the user wants to do. This type of software can be purchased or developed.
- The data access API (application programming interface) provides the interface between the application and the DBMS. Microsoft’s data access API is ADO.NET, which is a part of .NET.
- The processing that's done by the client software is typically referred to as front-end processing, and the client is typically referred to as the front end.

## The SQL interface

- The application software communicates with the DBMS by sending SQL queries through the data access API. When the DBMS receives a query, it provides a service like returning the requested data (the query results) to the client.
- SQL, which stands for Structured Query Language, is the standard language for working with a relational database.

Figure 19-2 The software components of a client/server system

## An introduction to relational databases

In 1970, Dr. E. F. Codd developed a model for what was then a new and revolutionary type of database called a relational database. This type of database eliminated some of the problems that were associated with standard files and other database designs. By using the relational model, you can reduce data redundancy, which saves disk storage and leads to efficient data retrieval. You can also view and manipulate data in a way that is both intuitive and efficient.

## How a table is organized

The model for a relational database states that data is stored in one or more tables. It also states that each table can be viewed as a two-dimensional matrix consisting of rows and columns. This is illustrated by the relational table in figure 19-3. Each row in this table contains information about a single product.

In practice, the rows and columns of a relational database table are sometimes referred to by the more traditional terms, records and fields. In fact, some software packages use one set of terms, some use the other, and some use a combination.

If a table contains one or more columns that uniquely identify each row in the table, you can define these columns as the primary key of the table. For instance, the primary key of the Products table in this figure is the ProductCode column.

In this example, the primary key consists of a single column. However, a primary key can also consist of two or more columns, in which case it’s called a composite primary key.

In addition to primary keys, some database management systems let you define additional keys that uniquely identify each row in a table, called non-primary keys. In SQL Server, these keys are also called unique keys, and they’re implemented by defining unique key constraints (also known simply as unique constraints). The only difference between a unique key and a primary key is that a unique key can be null and a primary key can’t.

Indexes provide an efficient way to access the rows in a table based on the values in one or more columns. Because applications typically access the rows in a table by referring to their key values, an index is automatically created for each key you define. However, you can define indexes for other columns as well. If, for example, you frequently need to sort the rows in the Products table by the Description column, you can set up an index for that column. Like a key, an index can include one or more columns.

## The Products table in the MMABooks database

![](img/844f608d10a44654833ea5efc8a2e7a7_641_0.png)

## Concepts

- A *relational database* uses *tables* to store and manipulate data. Each table consists of one or more *records*, or *rows*, that contain the data for a single entry. Each row contains one or more *fields*, or *columns*, with each column representing a single item of data.
- Most tables contain a *primary key* that uniquely identifies each row in the table. The primary key often consists of a single column, but it can also consist of two or more columns. If a primary key uses two or more columns, it’s called a *composite primary key*.
- In addition to primary keys, some database management systems let you define one or more *non-primary keys*. In SQL Server, these keys are called *unique keys*, and they’re implemented using *unique key constraints*. Like a primary key, a non-primary key uniquely identifies each row in the table.
- A table can also be defined with one or more *indexes*. An index provides an efficient way to access data from a table based on the values in specific columns. An index is automatically created for a table’s primary and non-primary keys.

## How the tables in a database are related

The tables in a relational database can be related to other tables by values in specific columns. The two tables shown in figure 19-4 illustrate this concept. Here, each row in an Invoices table is related to one or more rows in an InvoiceLineItems table. This is called a one-to-many relationship.

Typically, relationships exist between the primary key in one table and the foreign key in another table. The foreign key is simply one or more columns in a table that refer to a primary key in another table. In SQL Server, relationships can also exist between a unique key in one table and a foreign key in another table. For simplicity, though, this book only presents relationships that are based on primary keys.

Although it isn’t apparent in this figure, the InvoiceLineItems table has a composite primary key that consists of two columns: InvoiceID and ProductCode. As a result, any row in the InvoiceLineItems table can be uniquely identified by a combination of its invoice ID and product code. However, the InvoiceLineItems table can have more than one row for a given invoice ID and more than one row for a given product code.

One-to-many relationships are the most common type of database relationships. However, two tables can also have a one-to-one or many-to-many relationship. If a table has a one-to-one relationship with another table, the data in the two tables could be stored in a single table. Because of that, one-to-one relationships are used infrequently.

By contrast, a many-to-many relationship is usually implemented by using an intermediate table, called a linking table, that has a one-to-many relationship with the two tables in the many-to-many relationship. In other words, a many-to-many relationship can usually be broken down into two one-to-many relationships.
