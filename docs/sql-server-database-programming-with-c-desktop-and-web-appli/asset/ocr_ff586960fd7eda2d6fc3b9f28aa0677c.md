# Data Selection Query with Visual C#.NET

+   6) Call the suitable command/object using a SelectCommand (or the Fill()) or a DataReader to make data query.

+   7) Fill the data to the bound-controls on the Visual C# Form window.

+   8) Release the used OleDataAdapter. Command. DataTable and the DataReader objects.

+   9) Close the database Connection object if no database operation is needed.

Now let's develop a sample project to access the data using the runtime object for SQL Server 2019 Expression database via the Faculty Form.

# 5.15 QUERY USING RUNTIME OBJECT TO SQL SERVER DATABASE

As discussed in Chapter 3, one needs to use the different data providers to access the different databases, the ADO.NET provides different namespaces for three different data providers: System.Data.OleDb for OLEDB, System.Data.SqlClient for SQL Server and OracleClient for Oracle We divide this into two parts: 1) data query using the runtime object with general data query methods; 2) data query using runtime objects with the LINQ to SQL method. LINQ to SQL is a good technique that is supplied with Visual Studio 2018 and it is an API interface working with the SQL Server databases. We will first provide a detailed discussion about the general query methods for the SQL Server databases, and we will concentrate on the LINQ to SQL with another project. The reason for us to divide this into two parts is that the project using runtime objects and the SQL Server 2019 Expression database allows only a single database to be connected and applied for a data-application, meaning that it does not allow two or more users to access and use the same SQL Server 2019 Expression simultaneously. The first project we will develop is RSelectFactory which uses the general runtime objects and SQL command object to connect to our sample database file CSE_DEPT to perform the data query. The second project we will develop LINQSelfFactory Project which uses the LINQ to SQL technique and DataContext connected to the sample database to perform the similar operation. As we discussed in Chapter 4, the DataContext is a special class that provides a connection to the database and translates Query operators to the standard SQL statements to access our database. In order to access and use the same database simultaneously, we have to separate this into two parts with two different projects.

First's have a closer look at the Connection object with connection string.

# 5.15.1 CONNECT TO SQL SERVER 2019 EXPRESS DATabases

Basically, the similar runtime objects and structures are utilized to develop a data-driven project that can access the different databases. For example, three kind of data provider have a need to use the Connection, Command, Adapter and DataReader objects to perform data queries to either a DataSet or DataTable. The DataSet and the DataTable components are provider-independent, but the first four objects are provider-dependent. This means that one must use the prefixes to specify which kind of data provider is utilized for certain databases. A prefix would be used if a SQL Server database is utilized, such as SqlConnection, SqlCommand, SqlDataAdapter and SqlDataReader. The same rule will be applied to the other data provider, such as the Oracle provider.

Thus, the differences between the data-driven applications that can access the different database are the provider-dependent components. Among them, the Connection String is a big issue. Different data providers need to use different connection strings to make the correct connection to the associated database.