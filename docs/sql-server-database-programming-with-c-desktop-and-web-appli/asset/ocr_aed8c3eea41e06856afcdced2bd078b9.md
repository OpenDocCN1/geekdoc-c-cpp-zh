# Introduction to Language Integrated Query (LINQ)

| RowSetFieldLINQ.Program | Main() |

```
using System;
using System.Data;
using System.Data.OleDb;
using System.Linq;
namespace DataRowSetFieldLINQ
{
    class Program
    {
        static void Main(string[] args)
        {
            string cmd = "SELECT * FROM Faculty";
            OleDbDataAdapter adapter = new OleDbDataAdapter(cmd);
            OleDbConnection connection = new OleDbConnection();
            OleDbCommand command = new OleDbCommand();
            DataSet ds = new DataSet();
            string connString = "Provider=OleDb;Data Source=DESKTOP-24JPUFB\SQL2019EXPRESS;Database=CSE_DBPT;User ID=SMART;Password=Happy2022";
            connection = new OleDbConnection(connString);
            connection.Open();
            command.Connection = connection;
            command.CommandType = CommandType.Text;
            adapter.SelectCommand = command;
            adapter.Fill(ds
```

**4.41** The codes for the example DataRowSetFieldLINQ.

+   E. The Console.WriteLine method is executed to display both original and the current values of the DataColumn object faculty_name in the faculty table.
F. The database connection is closed after this query is done.

Before you can run the project to finish it, you must install the **System.Data.OleDb** package into the project to enable us to use some components located at that package. Refer to Section 5.4.1.3 to install this package with the Package Manager Console by going to the menu items **NuGet | Package Manager | Package Manager Console**.

Now you can run the project to test the functionality of the method SetChanged(). Click on the **Debug | Start Without Debugging** menu to run the project. You will find that both the original and the current version of the DataColumn object faculty_name is retrieved and displayed in the console window.

A complete C# project named DataRowSetFieldLINQ can be found from Class B Projects/Chapter 4 that is located under the Students folder at the CRC Fps fit site (refer to Figure 1.2 in Chapter 1).