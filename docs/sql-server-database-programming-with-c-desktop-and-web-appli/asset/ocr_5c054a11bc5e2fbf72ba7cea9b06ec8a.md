# Introduction to Language Integrated Query (LINQ)

| DataRowFieldLINQ.Program | Main() |

```
using System;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
namespace DataRowFieldLINQ
{
    class Program
    {
        static void Main(string[] args)
        {
            string cmdString = "SELECT * FROM Faculty";
            SqlDataAdapter dataAdapter = new SqlDataAdapter(cmdString);
            SqlConnection connection = new SqlConnection();
            SqlCommand command = new SqlCommand(connection);
            DataSet ds = new DataSet();
            string sqlString = "Server-DESKTOP-24JPUFB\SQL2019-CSE;" +
                "Initial Catalog=CSE_DEPT;" + " User ID=SMART;Password=Happy2022";
            connection = new SqlConnection(sqlString);
            connection.Open();
            command.Connection = connection;
            command.CommandType = Command.Text;
            command.CommandText = cmdString;
            dataAdapter.SelectCommand = command;
            dataAdapter.Fill(ds, "Faculty");
            DataTable dt = ds.Tables["Faculty"];
            IEnumerable<DataRow> row = dt.AsEnumerable();
            foreach (DataRow row in row)
            {
                if (row.Field<string>("faculty_name").Equals("Ying Bail\n                {
                    int FacultyID = row.Field<int>(dt.Columns[0]);
                    Console.WriteLine("The Selected Faculty ID: " + FacultyID + ");");
                }
            }
            connection.Close();
        }
    }
}
```

**FIGURE 4.40** The codes for the example DataDataFieldLINQ.

Now let's create a new C# project to illustrate how the Field() method to retrieve some columns' values from the DataRow object. The database we will use is our database-CSE DEPT. Open Visual .NET 2022 and create a new C# project and name it as DataRowFieldLINQ. Open the code window of the # Program.cs file and enter the codes that are shown in Figure 4.40 in this code window.

Let's have a closer look at this piece of code to see how it works.

+   A. Two namespaces, System.Data and System.Data.SqlClient, must be added into the namespace declaration of this project since we need to use some SQL data components as DataAdapter, Command and Connection.
B. A SQL query is used to query all columns from the Faculty table in the DataSet. Also all SQL related data components are created in this part including a non-SQL component, DataSet.
C. The connection string is declared since we need to use it to connect to our sample database CSE_DEPT which is developed in Microsoft SQL Server 2019. You need to modify this string based on the real server in which you save your database.