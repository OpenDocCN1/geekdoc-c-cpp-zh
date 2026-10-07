
# SQL Server Database Programming with C#

| DataSetSingleTableLINQ.Program | Main() |
|---|---|

```sharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Linq;
namespace DataSetSingleTableLINQ
```

```sharp
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

the foreach loop. Deferred query evaluation allows queries to be kept as values that be executed multiple times, each time yielding potential results.
I. Finally, the connection to our database is started by clicking the Close() method.

Now you can build and run this project by clicking Debug | Start Without Debugging. Retrieved information for the selected C# project will be retrieved and displayed in the console window.
A complete C# project named DataSetSingleTableLINQ can be found from a folder Class DB Objects\ Chapter 4 is located under the Students folder at the CRC ftp site (refer to Figure 1.2 in Chapter 1).

## 4.5.1.4 Query Cross Tables

A DataSet object must first be populated before you query it with LINQ to Data. The example we discussed in the last section, there are several ways to populate the DataSet. We used the DataAdapter class with the Fill method to do this operation. 

In addition to querying a single table, you can also perform cross queries in LINQ to DataSet. This is done using a join clause. A join is the association of objects in one data source that share a common attribute in another data source, such as a faculty_id in the Login table and the Faculty table. In object-oriented programming, relationships between objects are relatively easy to navigate because each object has a member that references another. In external database tables, however, navigating relationships is not straightforward. Database tables do not contain built-in relationships. In these cases, the Join operation can be used to match elements from each source. For example, given two tables that contain faculty information and course information, you could use a join operation to match course information and faculty for the same faculty_id.

The Language-Integrated Query (LINQ) framework provides two join operations, Join and GroupJoin. These operators perform query-joins: that is, joins that match two data sources only when their keys are equal. (By contrast, Transact-SQL supports operators other than equals, such as the less operator.)

In relational database terms, Join implements an inner join. An inner join is a type of join in which only objects that have a match in the opposite data set are returned.

In this section, we use an example project to illustrate how to use Join operator to perform a multi-table query using LINQ to DataSet. The functionality of this project is:

- 1) Produce a DataSet instance, exactly populate two tables, Faculty and Course, with two DataAdapters.
- 2) Using LINQ to DataSet join query to perform the cross-table query.

Now create a new C# project and name it DataSetCrossTableLINQ. Open the code window of Program.cs and enter the code shown in Figure 4.36 into this window.
Let's have a look at this piece of code to see how it works.

- A. Two names, System.Data and System.Data.OleDb, must be added to the namespace declaration of this project where we need to use some OleDb data components as DataAdapter, Command and Connection.
- B. Two SQL query strings are executed to query some columns from the Faculty and Course data tables in the DataSet. In addition, all OleDb data components, are created in this project, including a non-OleDb data component, DataSet. Each set of components is used to fill an associated data table in the DataSet.
- C. The connection string is declared when we use a SQL OleDb provider to connect to our sample database CSE_DEPT that was created with Microsoft SQL Server 2019. You may modify this string on the real server where you saved your database.
- D. The connection object is initialized with the connection string and connection is executed by calling the Open() method. Regularly a try-catch block should be used for this connection to catch any possible exception. Here we keep it since to make this connection coding initialized.
- E. The FacultyCommand object is initialized with Connection, CommandType and Text properties.
- F. The initialized facultyCommand object is assigned to the SelectCommand property of the facultyAdapter and the DataSet is filled with the Fill() method. The point is that only a single table, Faculty, is filled in this operation.
- G. The CourseCommand is initialized with Connection, CommandType and Text properties. The initialized courseCommand object is assigned to the SelectCommand property of the courseAdapter and the DataSet is filled with the Fill() method. The point is that only a single table, course, is filled in this operation.
- H. Two DataTable objects, faculty and course, are created and mapped to the DataSet.
- I. A LINQ to DataSet query is executed with a join clause. The data type of the query variable course is implicit and can be inferred as the project is compiled. Two data tables, Faculty and Course, work as a joined source for this LINQ to DataSet query; therefore, the AsEnumerable() method must be used to convert them to an IEnumerable<T> type. Two identical fields, faculty_id, is a primary key in the Faculty table and a foreign...

# SQL Server Database Programming with C#

# DataSetCrossTableLINQ.Program

```sharp
using System;
using System.Data;
using System.Data.OleDb;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace DataSetCrossTableLINQ
{
    class Program
    {
        static void Main(string[] args)
        {
            string faculty = "SELECT faculty_id, faculty_name FROM Faculty";
            string course = "SELECT faculty_id, course_id FROM Course";
            OleDbDataAdapter facultyAdapter = new OleDbDataAdapter();
            OleDbDataAdapter courseAdapter = new OleDbDataAdapter();
            OleDbConnection connection = new OleDbConnection();
            OleDbCommand facultyCommand = new OleDbCommand();
            OleDbCommand courseCommand = new OleDbCommand();
            DataSet ds = new DataSet();
            string connectionString = "Provider=SQL OLEDB;" + "Data Source=DESKTOP-24JUPFB\SQLEXPRESS;" + "Database=CSE_DEPT;" + "User ID=SMART;" + "Password=Happy2022";
            connection.ConnectionString = connectionString;
            connection.Open();
            facultyCommand.Connection = connection;
            facultyCommand.CommandType = CommandType.Text;
            facultyCommand.CommandText = faculty;
            facultyAdapter.Command = facultyCommand;
            facultyAdapter.Fill(ds, "Faculty");
            courseCommand.Connection = connection;
            courseCommand.CommandType = CommandType.Text;
            courseCommand.CommandText = course;
            courseAdapter.SelectCommand = courseCommand;
            courseAdapter.Fill(ds, "Course");
            DataTable faculty = ds.Tables["Faculty"];
            DataTable course = ds.Tables["Course"];
            foreach (var courseinfo in course.AsEnumerable())
            {
                foreach (var facultyinfo in faculty.AsEnumerable())
                {
                    if (courseinfo.Field<string>("faculty_id") == facultyinfo.Field<string>("faculty_id") && facultyinfo.Field<string>("faculty_name") == "Ying Bai")
                    {
                        string course_id = courseinfo.Field<string>("course_id");
                        foreach (var var in courseinfo)
                        {
                            Console.WriteLine(var[0] + ":" + course_id);
                        }
                    }
                }
            }
            connection.Close();
            facultyCommand.Dispose();
            courseCommand.Dispose();
            facultyAdapter.Dispose();
            courseAdapter.Dispose();
        }
    }
}
```

FIGURE 4.36 The code for the example project DataSetCrossTableLINQ.
