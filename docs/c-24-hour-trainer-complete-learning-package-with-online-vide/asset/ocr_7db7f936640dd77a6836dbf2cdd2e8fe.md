After you build the model, Visual Studio generates the classes you need. Now you just need to add code to use them.

If you are using a Microsoft Access database, start by adding the following using directive at the top of the file:

```
```csharp
using System.Data.OleDb;
```
```

The connection object that you need to open the database is defined in this namespace. (For other kinds of databases, you may need to use different database objects in other namespaces.)

Next build a database connection. The Linq To Access example program that is available in this lesson’s download uses the following code to build its connection:

```
```csharp
// Get the database's location.
string filename = Path.GetFullPath(
    Application.StartupPath + @"\..\..\CustomerData.mdb");

// Connect to the database.
using OleDbConnection conn = new OleDbConnection(
    "Provider=Microsoft.Jet.OLEDB.4.0;" +
    "Data Source=" + filename)
{
```
```

This program assumes the CustomerData.mdb database is located two directory levels above where the program is executing. This is true if the program is running from its bin\Debug directory and the database is stored with the code.

The program gets the location of the database file. It creates a new OleDbConnection object, passing its constructor a connect string that includes the location of the database file. (Connect strings for different kinds of databases hold different fields. If you’re using some other kind of database, you’ll need to build an appropriate connect string.)

Having connected to the database, the program should create an instance of the LINQ to SQL database class, passing its constructor the database connection. The Linq To Access example program uses the following code:

```
```csharp
// Get the database.
using (CustomerClassesDataContext db =
    new CustomerClassesDataContext(conn))
{
```
```

From this point on, the code is the same as it is for working with SQL Server. The only complication is that not all databases are created equal. Different databases may provide different features and the automatically generated database code may not work properly for all databases.

The Linq To Access example program executes the same queries as the Find Customers example and has no trouble until the final query, which adds 30 days to the customer’s due date. Access cannot understand the automatically generated code for that query and throws an exception.