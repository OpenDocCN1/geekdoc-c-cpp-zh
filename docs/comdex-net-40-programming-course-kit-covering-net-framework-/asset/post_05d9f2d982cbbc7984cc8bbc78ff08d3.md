
### Logical Operators

You can also use logical operators on the clauses used in SQL statements. For example, you can use logical operators when you are specifying two criteria in a SQL statement. First, the City field cannot be London or Barcelona, and second, there must be some value in the Fax field. To retrieve the records on the basis of these two criteria, you can use the following SQL command:

```sql
SELECT * FROM Customers WHERE City NOT IN ('London', 'Barcelona')
AND Fax IS NOT NULL
```

![](img/9862a98a1a2d3bb14334137965a1ec60_363_0.png)

> In the preceding query, we are using the NULL keyword to test whether the Fax field in the Customers table contains a value or not.

The different logical operators that you can use with the WHERE clause are as follows:

- **AND**: Specifies that both conditions in the **WHERE** clause must be **True**
- **OR**: Specifies that at least one of the conditions in the **WHERE** clause should be **True**
- **NOT**: Specifies that the condition in the **WHERE** clause should be **False**

### The ORDER BY Clause

You can also arrange the records in an order in the output by using the **ORDER BY** clause. For example, to retrieve the records in an ascending order of **CustomerID** from the **Customers** table, you can use the ORDER BY clause, as shown in the following SQL statement:

```sql
SELECT * FROM Customers ORDER BY CustomerID
```

You can also retrieve the records in descending order of **CustomerID** from the **Customers** table by using the DESC keyword, as shown in the following SQL statement:

```sql
SELECT * FROM Customers ORDER BY CustomerID DESC
```

![](img/9862a98a1a2d3bb14334137965a1ec60_363_1.png)

> If you are not providing the DESC keyword with the ORDER BY clause, by default, it returns results in an ascending order.

### The AS Clause

When you access records from a table, you can refer to the fields with some more descriptive names by using the AS clause. For example, referring to the Name field of a table as Name might be more descriptive for the user to understand than referring to the same field as **au_lname**. You can alias a field name with the AS clause. For example, you can use the following SQL statement to retrieve values of the **ContactName** field from the **Customers** table with the field name **ContactName** changed to **Name**:

```sql
SELECT ContactName AS Name FROM Customers
```

### Built-in Functions

SQL provides various built-in functions that help in performing arithmetic operations. These functions make it easier for you to query the data or perform operations on it. Some built-in functions provided by SQL are as follows:

- **COUNT()**: Returns the number of total records
- **SUM()**: Returns the sum of the values of a specified field
- **MIN()**: Returns the minimum of the values of a specified field
- **MAX()**: Returns the maximum of the values of a specified field
- **AVG()**: Returns the average of the values of a specified field

For example, you can use the **COUNT** function in a SQL statement as follows:

```sql
Select count(*) from Customers
```

The preceding query returns the count of the total number of records in the **Customers** table.

### The GROUP BY Clause

The GROUP BY clause is used to group some records according to the fields of a table. You can group records in SQL with the GROUP BY clause, as shown in the following SQL query statement:

```sql
SELECT OrderID, SUM(Quantity) FROM OrderDetails GROUP BY OrderID
```

In the preceding query, we have grouped the records in the OrderDetails table by the field OrderID. This means that we have grouped all the records that have the same OrderID.

### The HAVING Clause

The HAVING clause is used with the GROUP BY clause. The functionality of this clause is the same as that of the WHERE clause, but is used only with the GROUP BY clause. Using the HAVING clause, you can specify additional criteria for the records you want to retrieve. For example, to retrieve those records from the OrderDetails table for which the value in the Quantity field is less than 100, you can use the HAVING clause, as shown in the following SQL statement:

```sql
SELECT OrderID, SUM(Quantity) FROM OrderDetails GROUP BY OrderID HAVING
SUM(Quantity)<100
```

### The DELETE Statement

The DELETE statement is used to delete records from a table. For example, to delete all the records from the Customers table for which the value in the City field is not New York, you can use the DELETE clause, as shown in the following SQL statement:

```sql
DELETE FROM Customers WHERE City NOT IN ('New York')
```

### The UPDATE Statement

You can use the UPDATE statement to update a database. In other words, you can update the existing records in one or more columns of a table as and when required by using the UPDATE statement. For example, to change the value in the City field to California in all the records where its value is New York, you can use the UPDATE statement, as shown in the following SQL statement:

```sql
UPDATE Customers SET City = 'California' WHERE City = 'New York'
```

### Joining Tables

You can also work with relational databases in SQL. Relational databases are used to relate data in multiple tables. Suppose you want to retrieve customer names from the Customers table and the IDs of the items ordered by the customers from the Orders table. For this purpose, you have to relate or join these two tables. You can relate these tables by using the CustomerID field, which is present in both the tables. This field acts as the primary key in the Customers table and as the foreign key in the Orders table. You can use the following SQL statement to retrieve the records according to the preceding mentioned criteria:

```sql
SELECT Customers.ContactName, Orders.OrderID FROM
Customers, Orders WHERE Customers.CustomerID =
Orders.CustomerID
```

Now, before knowing how to use the basic SQL statements in ADO.NET to retrieve and manipulate data, let's get an overview of ADO.NET and the basic operations performed in ADO.NET.

### Introducing ADO.NET

ADO.NET is the main data access system that C# 2010 uses to work with the data stored in the tables of databases. It uses a disconnected data architecture, which means that you can work with a copy of the data in the database. In a traditional data connection, the application stays connected with the database even when the application is not functioning; thereby, wasting database resources. In ADO.NET, the application connects to a database when it needs to pass some query to the database and disconnects immediately after the result of the query is saved locally. Therefore, disconnected data architecture is maintained in ADO.NET to reduce the load on servers.

The functioning of an ADO.NET application is implemented by using the classes that are found in **System.Data.dll** and these classes are integrated with the Extensible Markup Language (XML) classes found in **System.Xml.dll**. Some of the important features of ADO.NET are as follows:

- **Supports SQL Server 2008 SqlClient:** Provides support for new features of SQL Server 2008 Database Engine by introducing .NET Framework Data Provider for SQL Server (`System.Data.SqlClient`). You need to install .NET Framework 3.5 SP1 (or later) to use the SQL Server 2008 SqlClient with your .NET application.
- **Language-Integrated Query (LINQ):** Simplifies querying by eliminating the need of using a separate query language. LINQ to ADO.NET is a LINQ technology, which enables querying in ADO.NET by using the LINQ programming model. LINQ to ADO.NET consists of two related features: LINQ to DataSet and LINQ to SQL. LINQ to DataSet facilitates faster querying of data on the content of a dataset and LINQ to SQL enables you to directly query SQL Server databases.
- **LINQ to DataSet:** Provides LINQ capabilities for disconnected data (the data that is stored locally) stored in a dataset. LINQ to DataSet makes it easier and faster to query data cached in a DataSet object. DataSet objects are important as they allow users to use a copy of the data stored in the tables of a database, without actually getting connected to the database. The LINQ to DataSet feature enables you to work more productively.
- **LINQ to SQL:** Provides a runtime infrastructure to manage relational data as objects. You can use the LINQ to SQL technology to translate a query into a SQL query and then use it to query data contained in tables of a SQL Server database. LINQ to SQL supports all the key functions that you like to perform while working with SQL, that is, you can insert, update, and delete information from a table.
- **Entity Framework:** Allows you to access the data from a database through an object model instead of a relational model. The Entity Framework was first introduced in .NET Framework 3.5. It provides you a set of Entity Data Model (EDM) functions that help you to write less access code, reduce maintenance, make the structure of data user-friendly, and persist the data. You can use a data provider called EntityClient and a language called Entity SQL to interact with the Entity Framework directly.

![](img/9862a98a1a2d3bb14334137965a1ec60_365_0.png)

> You learn more about LINQ in Chapter 6, Language-Integrated Query.

Let's now focus on the new features and components of ADO.NET in .NET 4.0.

### Enhancements in ADO.NET

ADO.NET 4.0 introduces many new features for the Entity Framework to support better data access. These new features include the persistence storage, support for foreign keys, deferred or lazy loading, self-tracking entities, model-first development, built-in functions, model-defined functions, and better n-tier support. Let's discuss these new features introduced in Entity Framework 4.0 in detail.

- **Foreign Keys Support:** Simplifies the process of creating and modifying relationships between tables. Foreign keys allow you to set up the entity relationships using foreign keys directly.
- **Persistence Ignorance:** Helps you to use your own classes in an Entity Framework application, without introducing interfaces or elements that are specific to Entity Framework.
- **Deferred or Lazy Loading:** Loads the related entities or objects automatically when they are accessed through a navigation property. This feature helps in improving the efficiency of an operation of a program. In Entity Framework, the lazy loading feature can be implemented by setting the **DeferredLoadingEnabled** property to true (which by default is set to false).
- **Support for Plain-Old Common Language Runtime Objects (POCOs):** Allows you to create classes that are not only simple, but can also be included in the Entity Framework. POCO helps the Entity Framework to use custom data classes along with the data model without making any changes to the data classes.
