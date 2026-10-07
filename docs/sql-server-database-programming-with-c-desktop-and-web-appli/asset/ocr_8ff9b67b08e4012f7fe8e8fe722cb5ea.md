# SQL Server Database Programming with C#

# DataSetCrossTableLINQ.Program

```
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
            OleDbDataAdapter adapter = new OleDbDataAdapter();
            OleDbDataAdapter adapter = new OleDbDataAdapter();
            OleDb connection = new OleDbConnection();
            OleDbCommand command = new OleDbCommand();
            OleDbCommand command = new OleDbCommand();
            DataSet ds = new DataSet();
            string connection = "Provider=SQL OLEDB;" + "Data Source=DESKTOP-24JUPFB\SQLEXPRESS;" + "Database=CSE_DBE;" + "User ID=SMART;" + "Password=Happy2022";
            connection.ConnectionString = connection;
            connection.Open();
            facultyCommand.Connection = connection;
            facultyCommand.CommandType = CommandType.Text;
            facultyCommand.CommandText = faculty;
            facultyAdapter.Command = facultyCommand;
            facultyAdapter.Fill(ds, "Faculty");
            courseCommand.Connection = connection;
            courseCommand.CommandType = CommandType.Text;
            courseCommand.CommandText = course;
            courseCommand.SelectCommand = courseCommand;
            courseAdapter.Fill(ds, "Course");
            DataTable faculty = ds.Tables["Faculty"];
            DataTable course = ds.Tables["Course"];
            foreach (var courseinfo in course.AsEnumerable())
            {
                foreach (var facultyinfo in faculty.AsEnumerable())
                {
                    if (courseinfo.Field<string>("faculty_id") == facultyinfo.Field<string>("faculty_id") && facultyinfo.Field<string>("faculty_name") == "Ying Bai")
                    {
                        course_id = courseinfo.Field<string>("course_id");
                        foreach (var var in courseinfo)
                        {
                            Console.WriteLine(var.id + ":" + course_id);
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