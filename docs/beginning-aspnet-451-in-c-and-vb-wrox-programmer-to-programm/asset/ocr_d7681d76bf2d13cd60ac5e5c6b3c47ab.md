whose names contain the capital S and order them in ascending order. It should come as no surprise that in this example, the Label control displays my name and of Scott Hanselman because only those two names match the Where criterion. Notice how in C# the code imports the System namespace. It is necessary to bring the LINQ functionality into scope for application. If you're finding that some keywords do not show up in IntelliSense or VS gives you compilation errors on your LINQ queries, check that you have this namespace imported at the top of your code file. In a VB website, this namespace is included by default.

Of course, this example is only the beginning. The different types of LINQ discussed in the following three sections enable you to create much more powerful queries against a wide variety of data sources.

Because LINQ is so powerful and has so much potential, it has been integrated into many different areas of the .NET Framework. The following sections introduce different LINQ implementations.

# LINQ to Objects

This is the purest form of language integration. With LINQ to Objects, you can query collections in your .NET applications as you saw in the previous example. You're not limited to arrays because LINQ enables you to query almost any kind of collection that exists in the .NET Framework.

# LINQ to XML

LINQ to XML is the new .NET way to read and write XML. Instead of typical XML query languages like XSLT or XPath, you can now write LINQ queries that target XML directly in your application.

# LINQ to ADO.NET

ADO.NET is the part of the .NET Framework that enables you to access data and use services like SQL Server and many other kinds of data sources. ADO.NET is also used under the hood by the SqlDataSource control and is commonly used in "raw data access code"—written in C# or VB that connects to a database without using the declarative controls. With LINQ you can query database-related information sets, including LINQ to DataSet, LINQ to SQL, and LINQ to Entities.

LINQ to DataSet allows you to write queries using the DataSet, a class that represents an in-memory version of a database.

LINQ to SQL allows you to write object-oriented queries in .NET projects that target Microsoft SQL Server databases. The LINQ to SQL implementation translates your queries into SQL statements, which are then sent to the database to perform typical CRUD operations. In the 3.5 version of this book, entire chapter was devoted to LINQ to SQL. However, Microsoft has indicated that it will not actively develop LINQ to SQL It will remain part of the .NET Framework and Visual Studio for the foreseeable future, but Microsoft won't be adding new functionality to it. Entity Framework (EF). Almost anything you can do in LINQ to SQL can be done in LINQ to Entities.