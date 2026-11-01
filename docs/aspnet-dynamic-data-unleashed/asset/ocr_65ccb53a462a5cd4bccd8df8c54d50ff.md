# CHAPTER 2

# Entity Framework

# IN THIS CHAPTER

+   - Understanding Entity Model
+   - LINQ to Entities
+   - Entity Lifecycle
+   - Entity Model in Depth
+   - Stored Procedures

Although it is possible to build ASP.NET Dynamic Data applications with plain ADO.NET data access components, some of its features, such as foreign key templates and filtering, require a modern, LINQ-enabled data access framework such as LINQ to SQL or Entity Framework.

LINQ to SQL was introduced in Visual Studio 2008 and .NET Framework 3.5 as a database-specific implementation of LINQ—Language Integrated Query functionality in C# and Visual Basic. LINQ allows developers to use SQL-like queries directly in the application code as opposed to calling stored procedures or passing SQL statements as strings for execution to a database server. LINQ to SQL was quickly followed by the ADO.NET Entity Framework, released with .NET Framework 3.5 Service Pack 1. LINQ to SQL was designed for simplicity and close integration with Microsoft SQL Server; the Entity Framework was designed for maximum flexibility and multiple database platforms.

Although LINQ-based data access code is much simpler than the traditional code based on ADO.NET, it represents a significant paradigm shift compared to the approach .NET and database developers have been trained to use for over a decade. The ways you retrieve and manipulate data and the way you submit changes and implement business logic are very different with LINQ-based data access frameworks, and using some of the old tricks and habits can lead you in the direction where you are fighting the framework instead of letting it help you.

Because the ASP.NET Dynamic Data relies heavily on LINQ, developers need to have a working knowledge of the underlying data access framework to understand how its web controls work and how to customize them effectively.