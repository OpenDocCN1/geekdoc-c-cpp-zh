Just as LINQ to XML added XML-specific extensions, LINQ to DataSet also adds several DataSet specific extensions. These extensions make it easier to query over a set of DataRow objects, enabling you to compare sequences of rows or directly access the column values of a DataRow.

![](bbox=[0.8, 0.22, 0.96, 0.27])

# ### Required References

To use LINQ to DataSet, you need to ensure that the project has references to the following assemblies:

+   - `System.Core`
- `System.Data`
- `System.Data.DataSetExtensions`
- `System.Data.Common` or `System.Data.SqlClient`, depending on how you connect to the database

You also need to include the `System.Linq` and `System.Data` namespaces.

# ## LINQ to SQL

LINQ to SQL enables you to write queries directly against SQL databases using the same query syntax you use for an in-memory collection or any other LINQ data source. Although ADO.NET maps the database to a conceptual data model, represented by a DataSet, LINQ to SQL maps directly to an object model in your application code. When your application executes, the LINQ syntax queries are translated by LINQ to SQL into SQL language queries that are then sent to the database to be executed. When the results are returned, LINQ to SQL translates them back to data model objects.

To use LINQ to SQL, you must first create the object model that represents the database. There are two ways to do this:

+   - The Object Relational Designer (O/R Designer), which is part of Visual Studio 2010, provides a rich user interface for creating the object model from an existing database. The O/R Designer supports only SQL Server Express, SQL Server 2000, 2005, and 2008 databases.
- The SQLMetal command-line tool, which should be used for large databases, or databases that the O/R Designer does not support.

When you decide how you will generate the object model, you need to decide what type of code you want to generate. Using the O/R Designer, you can generate C#