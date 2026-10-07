# SQL Server Database Programming with C#

| DataSetSingleTableLINQ.Program | Main() |
|---|---|

```
using System;
using System.Data;
using System.Data.ODb;
using System.Linq;
namespace DataSetSingleTableLINQ
```

```
class Program
{
    static void Main(string[] args)
    {
        string cmdString = "SELECT * FROM Faculty";
        ODbDataAdapter dataAdapter = new ODbDataAdapter();
        ODbConnection connection = new ODbConnection();
        ODbCommand command = new ODbCommand();
        DataSet ds = new DataSet();
        string ele = "Provider=SQOLEDB;Data Source=DESKTOP-24JUPFB;SQL2019EXPRESS;" + 
                      "Database=CSE_DEPT;User ID=SMART;Password=Happy2022";
        connection.ConnectionString = ele;
        connection.Open();
        dataAdapter.Connection = connection;
        command.CommandType = CommandType.Text;
        command.CommandText = cmdString;
        dataAdapter.SelectCommand = command;
        dataAdapter.Fill(ds
```

FIGURE 4.35 The codes for the example DataSetSingleTableLINQ.

the foreach loop. Deferred query evaluation allows queries to be kept as values that be
executed multiple times, each time yielding potential results.
I. Finally, the connection to our database is started by clicking the Close(class) method.

Now you can build and run this project by clicking Debug | Start Without Debugging. Retrieved information- for the selected C# project will be retrieved and displayed in the console window.
A complete C# project named DataSetSingleTableLINQ can be found from a folder Class
DB Objects\ Chapter 4 is located under the Students folder at the CRC ftp site (refer to
Figure 1.2 in Chapter 1).

# 4.5.1.4 Query Cross Tables

A DataSet object must first be populated before you query it with LINQ to Data. The example we discussed in the last
section, there are several ways to populate the DataSet. We used the DataAdapter class with the Fill method to do this operation.
 addition to querying a single table, you can also perform cross queries in LINQ to
DataSet. This is done using a join clause. A join is the association of objects in one data source
objects that share a common attribute in another data source, such as a faculty_id in the Login
table and the Faculty table. In object-oriented programming, relationships between objects are rel-atively easy to navigate because each object has a member that references another. In external