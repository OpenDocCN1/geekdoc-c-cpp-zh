# Introduction to Language Integrated Query (LINQ)

so you must call the AsEnumerable method if you want to use the DataTable as a source in the **From**nclause of a LINQ query.

As discussed in Chapter 4.5.1, to perform LINQ to DataSet query, the first step is to create
instance of the DataSet and fill it with the data from the database. To fill a DataSet,
DataAdapter can be used with the `Fill()` method that attaches to DataAdapter. Each
DataAdapter can only be used to fill a single DataTable in a DataSet.

In this section, we build an example to query a single DataTable using the LINQ to DataSet.
Create a new C# Console project DataSetQueryLINQ. In this project, we need to use OleDb
Provider to access our SQL server database `CSE_DEPT`. Microsoft will need first of
proper to enable us to do this. Before we build our codes, we need to use this System.
**Data.OleDb** package in our project to use it of. Perform the following operations to
add this package to our project:

+   1) Go to the menu **Tools | NuGet Package Manager | Package Manager Console**.
2) In the opened Package Manager Console window at the bottom, type the command:
`Install-Package System.Data.OleDb` and press the Enter key on your keyboard.
3) Some Successful installations are displayed on that console when it is
done, which means that the package has been successfully installed and added into our
project, and we can use it.

Now open the code window of the C# Program.cs file and see the codes that are shown in Figure 4.35
to window. Let's take a closer look at this piece of code to see how it works.

+   A. Two namespaces, **System.Data** and **System.Data.OleDb**, must be added into this project
we need to use OleDb data components.
B. A SQL query is created to query all columns from the Faculty table in this part including a non-OleDb
DataSet. Also OleDb data components are created in this part including a data component, DataSet.
C. The connection string is created since we need to use a SQL OleDb provider to connect to
our sample database `CSE_DEPT` that is developed with Microsoft SQL Server 2019 Express.
You may modify this string based on the server where you saved the data.
D. The connection object **connection** is initialized with the connection string and that
nection is executed by the `Open()` method. Regularly a `try-catch` block should be used
for this connection operation to catch any possible exception. Here we skip it if we want
try to make this connection coding simple process.
E. The Command object is initialized with Connection, **CommandType** and CommandText
properties.
F. The initialized Command object is assigned to the **SqlCommand** property of the
DataAdapter and the DataSet is filled with the `Fill()` method. The point is that only a single
table, **Faculty**, is filled in this operation.
G. A LINQ query to DataSet query is created with three clauses, **from**, **where** and **select**. The
data type of the query is implicit and it can be inferred from the
compiler as the query is compiled. The Faculty table works as a data source for
is LINQ to DataSet query; therefore, the AsEnumerable() method must be used
to convert it an `IEnumerable<T>`. The `where` clause filters the desired information
the selected faculty member (**faculty_name**). All of these clauses will be converted
to the associated Standard Query Operator methods that will be used to perform
this query.
H. A foreach loop then enumerates the Enumerable object returned and yields the
query results. Since the query is an Enumerable type, it implements `IEnumerable<T>`,nand the evaluation of the query is deferred until the query variable is iterated over using