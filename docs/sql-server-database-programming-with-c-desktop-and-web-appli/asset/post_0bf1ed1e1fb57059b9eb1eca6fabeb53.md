
## Data Selection Query with Visual C#.NET

The third method is to use stored procedures to integrate multiple queries into a single function or to simplify the query operations and speed up the query processes. This method is especially useful for complicated query, in which multiple queries are needed to be performed to get the desired output results.

The fourth method, LINQ to SQL, is a good method and this technique was released with the Visual Studio .NET 2008. The coding process can be simplified and the query efficiency can be greatly improved by using this technique. These advantages can be found by comparing the queries we developed in this chapter.

A popular and powerful database is discussed in this chapter: Microsoft SQL Server Database, and it is explained in detail with some real sample projects. Different projects use different queries: DataAdapter method, retrieve method, stored procedure, and LINQ to SQL method. Line-by-line illustrations are provided for each sample project. The readers can obtain solid knowledge and practical experience how to develop a professional query application after they finish this chapter.

After finishing Part I in this chapter, you should be able to:

- Use the tools and wizards by develop simple data-driven applications to perform data query to Microsoft SQL Server 2019 database.
- Use the SqlConnection class to connect to Microsoft SQL Server 2019 Express database.
- Perform data binding to a DataGridView using two methods.
- Use the SqlCommand class to execute the data query with dynamic parameters to Microsoft SQL Server 2019 Express database.
- Use the SqlDataAdapter to fill a Dataset and a DataTable with Microsoft SQL Server 2019 Express database.
- Use the SqlDataReader class to query and process data with Microsoft SQL Server 2019 Express database.
- Use LINQ to SQL, to simplify the data query process and improve the data query efficiency.
- Set properties for the SqlCommand object to construct a desired query for Microsoft SQL Server 2019 Express database.

After reading Part II in this chapter, you should be able to:

- Use the runtime to develop the professional data-driven applications to perform data query to Microsoft SQL Server 2019 database.
- Use the SqlConnection class to dynamically connect to Microsoft SQL Server 2019 Express database.
- Use the SqlCommand class to dynamically execute the data query with dynamic parameters to Microsoft SQL Server 2019 Express database.
- Use the SqlDataAdapter to dynamically fill a Dataset and a DataTable with Microsoft SQL Server 2019 Express database.
- Use the SqlDataReader class to dynamically read and process data with Microsoft SQL Server 2019 Express database.
- Use LINQ to SQL to significantly simplify the query process and improve the query efficiency.
- Set properties for the SqlCommand object dynamically to construct a desired query string for Microsoft SQL Server 2019 Express database.
- Use the Server Explorer to create, debug and test procedures in Visual Studio.NET environment.
- Use SQL stored procedure to perform the data query from Visual C#.NET.
- Use the SQL nested procedure to perform the data query from Visual C#.NET.

## 304 SQL Server Database Programming with C#

In Chapter 6, we will discuss the insertion technique with Microsoft SQL Server 2019 database. Three methods are introduced in two parts: Part I: Using the Design Tools and Wizards provided by Visual Studio.NET to develop data inserting, and Part II: Using the Runtime objects and LINQ to SQL to perform the data insertion job for Microsoft SQL Server 2019 Express database.

## HOMEWORK

### I. TRUE/FALSE SECTIONS

1. Data Provider-dependent objects are Connection, Command, TableAdapter and DataReader.
2. LINQ to DataSet controls can be used to access any kind of databases.
3. To move between the bound controls on a form window and the associated columns in the data source, BindingSource is needed.
4. To set up the connection between the controls on a form window and the associated columns in the data source, TableAdapter is needed.
5. All Table classes are located in the namespace DataSetAdapters.
6. Running the Fill() method is equivalent to executing the Command.
7. The DataSet can be considered as a container that contains multiple data tables, but tables are only a mapping of method to fill a data table that is located in the database.
8. To run the Fill() method is exactly to fill a data table that is located in the DataSet, not a real data table in the database.
9. By checking the Count property of a data table, one can determine whether a table operation is successful or not.
10. The DataTable object is a Data Provider-independent object.
11. If one needs to include the SELECT statements in a SQL stored procedure, one can directly create a stored procedure and call it from Visual .NET.
12. In order to use LINQ to SQL query method, one must create an entity class for each data table located in the target database.
13. To directly create, edit, manipulate and test stored procedures for the SQL database inside Visual Studio.NET environment.
14. To call a SQL stored procedure, one must use the CommandType property of the Command object to Procedure.
15. To set up a dynamic parameter in a SELECT statement in the SQL database, a @ symbol must be prefixed before the nominal variable.
16. To access different databases using LINQ technique, different LINQ API is used. For example, to access the SQL Server database, LINQ to SQL is used, to access the Oracle database, LINQ to Oracle must be used.
17. To assign a parameter in a SELECT statement in the SQL database, the keyword LIKE must be used as the assignment operator.
18. Two popular tools used to create an entity class are: SQLMetal and Object Relational Designer.
19. Two popular ways to query data from any database are: using Fill() method that belongs to the TableAdapter class, or calling ExecuteReader method that belongs to the Class.
20. A DataTable can be considered as a collection of DataRowCollection and DataColumn Collection, and the latter contains DataRow and DataColumn objects.

## Data Selection Query with Visual C#.NET

### II. MULTIPLE CHOICES

1. To connect a database dynamically, one needs to use the \_\_\_\_\_
a. Data Source
b. TableAdapter
c. Runtime object
d. Tools and Wizards

2. Four popular data providers are
a. ODBC, DB2, JDBC and SQL
b. SQL, ODBC, DB2 and Oracle
c. ODBC, OLEDB, SQL and Oracle
d. Oracle, OLEDB, SQL and DB2

3. To modify the DataSet, one needs to use the \_\_\_\_\_\_ Wizard.
a. DataSet configuration
b. DataSet edit
c. TableAdapter configuration
d. Query Builder

4. To bind a control with the associated column in a data table, one needs to use \_\_\_\_\_\_
a. BindingNavigator
b. TableAdapter
c. DataSet
d. BindingSource

5. The \_\_\_\_\_\_\_\_\_\_\_ keyword should be used as an assignment operator for the WHERE clause with a dynamic parameter for a data query in SQL Server database.
a. = \_\_\_\_\_
b. LIKE
c. := \_\_\_\_\_
d. =@ \_\_\_\_\_

6. The \_\_\_\_\_\_\_\_\_\_\_ data provider can be used to execute the data query for \_\_\_\_\_\_\_\_\_\_\_ data providers.
a. SQL Server, OleDb and Oracle
b. OleDb, SQL Server and Oracle
c. Oracle, SQL Server and OleDb
d. SQL Server, Odbc and Oracle

7. To perform a Fill() method to fill a data table, exactly it executes \_\_\_\_\_\_\_\_\_\_\_ object with suitable parameters.
a. DataAdapter
b. Connection
c. DataReader
d. Command

8. To fill a list box or combobox control, one must \_\_\_\_\_\_\_\_\_\_\_ by using the \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ method.
a. Remove all old items, Remove()
b. Remove all old items, ClearBefore()
c. Clean up old items, ClearAll()
d. Clear all old items, ClearAll()

9. A \_\_\_\_\_\_\_\_\_\_\_ accessing mode should be used to define a connection object if one wants to use for the whole project.
a. Private, locally
b. Protected, globally
c. Public, locally
d. Public, globally
