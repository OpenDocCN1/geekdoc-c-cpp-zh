▪ **LINQ to Entities:** Allows you to write queries for the Entity Framework conceptual model, which enables users to visually design models and map databases, tables, and views by using Visual Studio 2010 and .NET Framework 4.0.

Let’s now discuss two of the important technologies in detail.

# ## LINQ to DataSet

A dataset is an in-memory representation of data that acts as the core of a wide variety of data-based applications. After data is loaded into a dataset, you often need to perform additional queries on the data. These additional queries are generally executed by using the LINQ to DataSet technology.

LINQ to DataSet provides an easier and faster way to query data cached in a dataset object as compared to traditional methods of querying the data. LINQ to DataSet simplifies the process of querying by enabling you to write queries in the programming language itself. The query operators allow you to perform LINQ queries on the dataset. To begin querying a dataset by using LINQ to DataSet, you need to confirm whether your dataset is filled with data or not because you cannot get any output or result set from an empty dataset.

Perform the following steps to implement LINQ to DataSet in a console application:

+   1. *Start* VisualStudio2010.
+   2. *Select* File→New→Project from the menu bar. The New Project dialog box opens.
+   3. *Select* Visual C#→Windows from the Installed Templates section in the left pane of the New Project dialog box. The project templates available for developing Windows-based applications in C# are displayed in the right pane of the New Project dialog box.
+   4. *Select* the Console Application template in the right pane to create a Windows Forms application.
+   5. *Enter* the name of the application as **LINQtoDataSet** (also available on the CD) in the Name text box and an appropriate location for the application in the Location combo box.
+   6. *Click* the **OK** button to close the New Project dialog box. The **LINQtoDataSet** application is created.
+   7. *Double-click* the **Program.cs** file in **Solution Explorer** to open the file in the Code Editor and add the highlighted code, given in Listing 6.18, to the Code Editor:

**Listing 6.18:** Showing the Code of the **Program.cs** File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Data;

namespace LINQtoDataset
{
    class Student
    {
        public int Id;
        public string Name;
    }

    class Program
    {
        static DataTable GetDataTable(Student[] students)
        {
            DataTable table = new DataTable();
            table.Columns.Add("Id", typeof(Int32));
            table.Columns.Add("Name", typeof(string));
            foreach (Student s in students)
            {
                table.Rows.Add(s.Id, s.Name);
            }
        }
    }
```