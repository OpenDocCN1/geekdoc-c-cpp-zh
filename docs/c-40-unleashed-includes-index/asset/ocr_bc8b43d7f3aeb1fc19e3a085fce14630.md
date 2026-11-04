To try this, we first create a data context in our Visual Studio 2010 project, exporting the metadata of the target database. This is the O/R part of the LINQ to SQL solution. After we've done so, we can write LINQ queries against the data source. Notice that there's also the so-called Entity Framework, which is the big brother to LINQ to SQL and the preferred way to query relational data today. We won't cover Entity Framework in this book and refer to specialized literature on the subject.

First, in Visual Studio 2010, we add a new item of type LINQ to SQL Classes to the current project, as shown in Figure 19.5.

![](bbox=[0.1, 0.36, 0.85, 0.66])

FIGURE 19.5 Object/relational mapping starts with a LINQ to SQL Classes item.

This brings up the Object Relational Designer, where we can use the Server Explorer to connect to a SQL Server database and drag and drop data sources (like tables, views, and stored procedures) to the designer surface. Doing so causes the designer to generate code that will make it easy to reach out to the database from code. Figure 19.6 shows the result after adding a few Northwind tables from the Server Explorer to the mapping surface.

# REQUIREMENTS FOR LINQ TO SQL SAMPLES

To run the LINQ to SQL examples, you'll need some SQL Server installation at your service. If you don't have such a server lying around, the free Express edition can be downloaded and installed on your development computer.

For the examples, I'm using the familiar Northwind database that came with the SQL Server product until version 2000. To install it on SQL Server 2005 or 2008, search the Web for "SQL Northwind Sample" to download the database with install scripts from the Microsoft download center. The installer merely unpacks the file into a folder called SQL Server 2000 Sample Databases, leaving the rest of the installation to you. Various approaches can be taken to execute the .sql file, one of which is the use of the sqlcmd.exe tool that comes with SQL Server:

```
sqlcmd -S . -E -i Northwind.sql
```