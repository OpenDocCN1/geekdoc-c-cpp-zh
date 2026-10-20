# An introduction to ADO.NET

ADO.NET (ActiveX Data Objects .NET) is the primary data access API for .NET. It provides classes to develop database applications with C# as well as other .NET languages. In the topics that follow, you’ll be introduced to the .NET data providers and the objects they provide for accessing databases.

# The .NET data providers

A .NET data provider is a set of classes that enables you to access data that’s managed by a particular database server. All .NET data providers must include core classes for creating the three types of objects listed in the first table in figure 21-1. You’ll learn more about how these objects work in the topics that follow.

The second table in this figure lists the three data providers for .NET. The SQL Server data provider is designed to provide efficient access to a Microsoft SQL Server database. The OLE DB data provider is a generic data provider that can access any database that supports the industry standard OLE DB interface. Although you can use the OLE DB data provider to access a SQL Server database, you shouldn’t do that unless you plan on migrating the data to another database since the SQL Server data provider is optimized for accessing SQL Server data. The ODBC provider lets you access any database that can work with ODBC, another industry standard database interface.

In addition to the three data providers shown in the second table, several other database vendors have developed .NET data providers that are optimized for use with their databases. For example, .NET data providers are available for the popular MySQL and Oracle databases. So, before you develop an application using the OLE DB or ODBC providers, you should check with your database vendor to see if a specialized .NET data provider is available.

The third table in this figure lists the names of the classes you use to create objects using the SQL Server, OLE DB, or ODBC provider. Notice that these classes use prefixes (“Sql,” “OleDb,” and “Odbc”) to indicate which provider each class belongs to.

The OLE DB and ODBC providers are installed as part of .NET Core. However, the SQL Server provider isn’t installed as part of .NET Core. As a result, to use the SQL Server provider, you must install the Microsoft.Data.SqlClient NuGet package. To do that, you can use the NuGet Package Manager as described in figure 20-2.

When you develop a C# application that uses ADO.NET, you’ll want to add a using directive for the namespace that contains the data provider classes at the beginning of each source file that uses those classes. That way, you won’t have to qualify the references to these classes. For example, if you’re using the SQL Server data provider, you’ll want to add a using directive like the one shown in this figure.