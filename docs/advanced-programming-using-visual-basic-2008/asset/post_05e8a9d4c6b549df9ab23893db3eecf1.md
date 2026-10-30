
## CHAPTER 3
## Windows Database Applications

At the completion of this chapter, you will be able to ...

+   1. Retrieve and display data from a SQL Server database on Windows Forms.
+   2. Use the ADO.NET data components: TableAdapters, DataSets, and DataConnectors.
+   3. Display database fields in a grid and in details view.
+   4. Sort database data using a method and an SQL query.
+   5. Concatenate data fields using SQL or the DataSet Designer.
+   6. Access data using a stored procedure.
+   7. Write a multitier application that separates the data tier from the presentation tier.
+   8. Declare and instantiate DataSet and TableAdapter objects in code and write the code to bind data to form controls.

In this chapter, you learn to access and display database data on a Windows form. You will follow good OOP principles and perform the database access in a data-tier component. You will learn to use table adapters and DataSets to display data from a database file. This chapter looks at the underlying SQL statements that retrieve the data and also introduces stored procedures. In Chapter 4 you will work with multiple related tables and in Chapter 5 you will learn to update a database.

### Visual Studio and Database Applications

Professional VB programmers spend the majority of their time on applications that involve databases. To be a good programmer, you will want to concentrate on the various methods of displaying and updating database information.

With VB you can create very simple database applications that require virtually no coding, all the way up to very powerful distributed applications that access and modify data on multiple large-scale servers. You can create programs that display and/or update data on a single stand-alone computer as well as multiuser networked databases. Although this text concentrates on SQL Server Express databases, the techniques that you learn also extend to larger-scale databases, such as SQL Server, Oracle, Sybase, and DB2. You also can apply most of the techniques in this chapter to an Access database.

The managed providers that ship with the .NET Framework are

+   - Microsoft Access Database File.
+   - Microsoft ODBC Data Source.
+   - Microsoft SQL Server Compact 3.5.
+   - Microsoft SQL Server Database File.
+   - Oracle Database (other database formats).

### ADO.NET

ActiveX Data Objects (ADO) .NET 3.5 is Microsoft's latest database object model. The goal of ADO.NET is to allow programmers to use a standard set of objects to refer to data from any source.

The trend toward accessing data from the Web and multiple platforms has changed the techniques that we use for data handling. In the past, it was common to connect to a database in a client/server format. The connection was kept open while the user browsed and/or updated the data, and data typing was not much of a concern. But now, using the .NET approach, we use disconnected DataSets with common data representation (data types) from multiple sources. The .NET Framework is also tightly integrated with Extensible Markup Language (XML), an industry-standard format for storing and transferring data over multiple platforms.

### Accessing Data in the .NET Framework

You will find a new world of terminology for working with data: data sources, data designers, datasets, binding sources, table adapters, and more. In addition, you will use many of the standard terms for data elements.

### Database Terminology

A data table can be viewed like a spreadsheet—with rows and columns. Each row in a table represents the data for one item, person, or transaction and is called a record. Each column in a table is used to store a different element of data, such as an account number, a name, address, or numeric amount. The elements represented in columns are called fields. You can think of the table in Figure 3.1 as consisting of rows and columns or of records and fields.

A table consists of rows (records) and columns (fields).

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_130_0.png)

Most tables use a primary key field (or combination of fields) to uniquely identify each record. The primary key field is often a number, such as employee number, account number, identification number, or social security number; or it may be a text field, such as last name, or a combination, such as last name and first name.

### Data Sources

Your application obtains data from a data source. You can create a data source from a large-scale database, a local database file, a Web service, or other types of objects. For local database files, which reside on the developer's computer, .NET currently supports Access .mdb and .accdb files and SQL Server Express .mdf files. SQL Server Express .mdf files are the recommended choice for Visual Basic. The Visual Studio environment allows you to create and edit SQL Server Express data sources.

When you create a data source from a database, a typed DataSet is added to your project. Each typed DataSet has a schema, which describes the fields and their data types. Although .NET provides for several kinds of data sources, we will concentrate on typed DataSets, which are the recommended approach for handling data in most situations.

### DataSet Objects

A DataSet object holds a copy of the data in memory, disconnected from the data source. You can consider a DataSet to be a temporary cache, rather than the actual database data.

A DataSet object can hold one or more tables. A relational database generally contains multiple tables and relationships between the tables. For example, an Employee table may have an Employee ID field and the Payroll table also will have an Employee ID field. The two tables are related by Employee ID. You can find the employee information for one payroll record by retrieving the record for the corresponding Employee ID. In the example in Figure 3.2, Employee ID is the primary key for the Employee table. The Employee ID field in the Payroll table is considered a foreign key—the field that links a Payroll record to its corresponding Employee record. So to retrieve the Employee’s name for a given Payroll record, for example, the foreign key is used to look up the corresponding record in the Employee table.

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_131_0.png)

Figure 3.2
The Employee table and Payroll table are related by Employee ID, which is the primary key in the Employee table and the foreign key in the Payroll table.

### The DataSet Object Model

Each DataSet object contains a DataTable collection, which is made up of individual DataTable objects. The DataTable object has both DataRow and DataColumn collections. A single DataRow holds the actual data for one record. The DataRow object maintains the original values and any changed values. This information is used to determine which rows have changed during program execution.

A DataRelation object stores information about related tables, including which columns contain the primary keys and foreign keys that link the tables. The Constraints collection, which belongs to the DataTable object, holds two types of Constraint objects: Unique constraints and ForeignKey constraints. Unique constraints enforce the requirement that values in the specified field be unique, which is usually required for primary key fields. ForeignKey constraints require that any foreign key value that appears in a secondary table match a primary key value in the primary table.

Figure 3.3 shows the object model of the DataSet object.
Note: See "Datasets in Visual Studio Overview" in Visual Studio Help.

### TableAdapters

A TableAdapter object provides the communication between your program and the database, sometimes called the "data access layer." A TableAdapter connects to the database and handles SQL queries and stored procedures, fills the DataSets, and handles writing any changes back in the data source.

One of the features of a TableAdapter is that it can hold multiple queries. You can retrieve the data by calling a specific query or by getting all of the data for the table. These TableAdapter objects have more functionality than the DataAdapters used in earlier editions of this text. (DataAdapters are still available in VB 2008.) The visual designers in the Visual Studio IDE automatically generate TableAdapters for you when you add a typed DataSet.
