
### Web Resources

For a list of covariant and contravariant interface types, visit

```
`https://msdn.microsoft.com/library/dd799517#VariantList`
```

It's also possible to create your own types that support covariance and contravariance. For information, visit

```
`https://msdn.microsoft.com/library/mt654058`
```

## 19.14 Wrap-Up

This chapter introduced the prepackaged collection classes provided by the .NET Framework. We presented the hierarchy of interfaces that many of the collection classes implement, overviewed many of the implementation classes and introduced enumerators that enable programs to iterate through collections.

We discussed the .NET Framework namespaces dedicated to collections, including System.Collections for object-based collections and System.Collections.Generic for generic collections—such as the List<T>, LinkedList<T>, Dictionary<K,V> and SortedDictionary<K,V> classes—that store objects of types you specify when you create the collection. We also mentioned the namespace System.Collections.Concurrent containing so-called thread-safe generic collections for use in multithreaded applications, and System.Collections.Specialized containing collections that are optimized for specific scenarios, such as manipulating collections of bits.

You saw how to use class Array to perform array manipulations. We continued our discussion of delegates that hold references to methods and introduced lambda expressions, which allow you to define anonymous methods that can be used with delegates. We focused on using lambdas to pass method references to methods that specify delegate parameters.

We provided a brief introduction to functional programming, showing how to use it to write code more concisely and with fewer bugs than programs written with previous techniques. In particular, we used LINQ extension methods and lambdas to implement functional operations that manipulated lists of values.

In Chapter 20, we begin our discussion of databases, which organize data in such a way that the data can be selected and updated quickly. We introduce the ADO.NET Entity Framework and LINQ to Entities, which allow you to write LINQ queries that are used to query databases.

- 20.1 Introduction
- 20.2 Relational Databases
- 20.3 A Books Database
- 20.4 LINQ to Entities and the ADO.NET Entity Framework
- 20.5 Querying a Database with LINQ
- 20.5.1 Creating the ADO.NET Entity Data Model Class Library
- 20.5.2 Creating a Windows Forms Project and Configuring It to Use the Entity Data Model
- 20.5.3 Data Bindings Between Controls and the Entity Data Model
- 20.6 Dynamically Binding Query Results
- 20.6.1 Creating the Display Query Results GUI
- 20.6.2 Coding the Display Query Results App
- 20.7 Retrieving Data from Multiple Tables with LINQ
- 20.8 Creating a Master/Detail View App
- 20.8.1 Creating the Master/Detail GUI
- 20.8.2 Coding the Master/Detail App
- 20.9 Address Book Case Study
- 20.9.1 Creating the Address Book App's GUI
- 20.9.2 Coding the Address Book App
- 20.10 Tools and Web Resources
- 20.11 Wrap-Up

## 20.1 Introduction

A database is an organized collection of data. A database management system (DBMS) provides mechanisms for storing, organizing, retrieving and modifying data. Many of today's most popular DBMSs manage *relational databases*, which organize data simply as tables with *rows* and *columns*.

Some popular proprietary DBMSs are Microsoft SQL Server, Oracle, Sybase and IBM DB2. PostgreSQL, MariaDB and MySQL are popular *open-source* DBMSs that can be downloaded and used *freely* by anyone. In this chapter, we use a version of Microsoft's SQL Server that's installed with Visual Studio. It also can be downloaded separately from

```
https://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/sql-server-express.aspx
```

### SQL Server Express

SQL Server Express provides many features of Microsoft's full (fee-based) SQL Server product, but has some limitations, such as a maximum database size of 10GB. A SQL Server Express database file can easily be migrated to a full version of SQL Server. You can learn more about the SQL Server versions at

```
https://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/overview.aspx
```

The version of SQL Server bundled with Visual Studio Community is called *SQL Server Express LocalDB*. It's meant for development and testing of apps on your computer.

### Structured Query Language (SQL)

A language called Structured Query Language (SQL)—pronounced “sequel”—is an international standard used with relational databases to perform queries (that is, to request information that satisfies given criteria) and to manipulate data. For years, programs that
accessed a relational database passed SQL queries as strings to the database management system, then processed the results.

### LINQ to Entities and the ADO.NET Entity Framework

A logical extension of querying and manipulating data in databases is to perform similar operations on *any* sources of data, such as arrays, collections (like the *Items* collection of a *ListBox*) and files. Chapter 9 introduced *LINQ to Objects* and used it to manipulate data stored in arrays. *LINQ to Entities* allows you to manipulate data stored in a relational database—in our case, a *SQL Server Express* database. As with *LINQ to Objects*, the IDE provides *IntelliSense* for your *LINQ to Entities* queries.

The ADO.NET Entity Framework (EF) enables apps to interact with data in various forms, including data stored in relational databases. You’ll use the ADO.NET Entity Framework and Visual Studio to create a so-called *entity data model* that represents the database, then use *LINQ to Entities* to manipulate objects in the *entity data model*. Though you’ll manipulate data in a *SQL Server Express* database in this chapter, the ADO.NET Entity Framework works with *most* popular database management systems. Behind the scenes, the ADO.NET Entity Framework generates SQL statements that interact with a database.

This chapter introduces general concepts of relational databases, then implements several database apps using the ADO.NET Entity Framework, *LINQ to Entities* and the IDE’s tools for working with databases. Databases are at the heart of most “industrial strength” apps.

## 20.2 Relational Databases

A relational database organizes data in tables. *Figure 20.1* illustrates a sample *Employees* table that might be used in a personnel system. The table stores the attributes of employees. Tables are composed of rows (also called *records*) and columns (also called *fields*) in which values are stored. This table consists of six rows (one per employee) and five columns (one per attribute). The attributes are the employee’s

- ID,
- name,
- department,
- salary and
- location.

The *ID* column of each row is the table’s *primary key*—a column (or group of columns) requiring a *unique* value that cannot be duplicated in other rows. This guarantees that each primary-key value can be used to identify *one row*. A primary key composed of two or more columns is known as a *composite key*—in this case, every combination of column values in the composite key must be unique. Good examples of primary-key columns in other apps are a book’s ISBN number in a book information system or a part number in an inventory system—values in each of these columns must be unique. We show an example of a composite primary key in Section 20.3. *LINQ to Entities requires every table to have a primary key* to support updating data in tables. The rows in

| ID | Name | Department | Salary | Location |
|---:|---|---:|---:|---|
| 23603 | Jones | 413 | 1100 | New Jersey |
| 24568 | Kerwin | 413 | 2000 | New Jersey |
| 34589 | Larson | 642 | 1800 | Los Angeles |
| 35761 | Myers | 411 | 1400 | Orlando |
| 47132 | Neumann | 413 | 9000 | New Jersey |
| 78321 | Stephens | 611 | 8500 | Orlando |

_Row_ — Primary key: ID; _Column_ — Department

**Fig. 20.1** | Employees table sample data.

Rows in Fig. 20.1 are displayed in *ascending* order by primary key. But they could be listed in *descending* order or in no particular order at all.

Each column represents a different data *attribute*. Some column values may be duplicated between rows. For example, three different rows in the Employees table’s Department column contain the number 413, indicating that these employees work in the same department.

### Selecting Data Subsets

You can use LINQ to Entities to define queries that select subsets of the data from a table. For example, a program might select data from the Employees table to create a query result that shows where each department is located, in ascending order by Department number (Fig. 20.2).

| Department | Location |
|---:|---|
| 413 | New Jersey |
| 611 | Orlando |
| 642 | Los Angeles |

**Fig. 20.2** | Distinct Department and Location data from the Employees table.

## 20.3 A Books Database

We now consider a simple Books database that stores information about some Deitel books. First, we overview the database’s tables. A database’s tables, their fields and the relationships among them are collectively known as a database schema. The ADO.NET Entity Framework uses a database’s schema to define classes that enable you to interact with the database. Sections 20.5–20.8.2 show how to manipulate the Books database. The database file—Books.mdf—is provided with this chapter’s examples. SQL Server database files have the .mdf (“master data file”) filename extension.

### Authors Table

The database consists of three tables: Authors, Titles and AuthorISBN. The Authors table (described in Fig. 20.3) consists of three columns that maintain each author’s unique
