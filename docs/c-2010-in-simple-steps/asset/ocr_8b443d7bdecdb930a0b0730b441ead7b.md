# Programming with LINQ to DataSet

A dataset is a very useful in-memory representation of data and acts as a core for a wide variety of data-based applications. After data is loaded into a dataset, you often need to perform additional queries on the data, and this is where LINQ to DataSet comes into play.

LINQ to DataSet enables .NET developers to query data cached in a dataset object. It simplifies querying by enabling you to write and execute queries directly from a .NET application by using any of the .NET languages, such as C# and VB.NET. You can implement LINQ to DataSet by using different query operators.

The first step before you begin querying a dataset by using LINQ to DataSet is to populate the dataset with data. After loading the data, you can begin executing queries on the data.

Now, let's create a console application called LINQtoDataset, to show the implementation of LINQ to DataSet, by performing the following steps:

+   1. Repeat steps 1 and 2 shown earlier while creating the LINQQuery application in the Explaining LINQ Queries and Their Execution section of this chapter.
+   2. Select the Visual C#→Windows option in the Installed Templates pane and the Console Application option in the middle pane of the New Project dialog box.
+   3. Enter LINQtoDataset in the Name text box to specify the name of the application, and enter an appropriate location for the application in the Location combo box.
+   4. Click the OK button. The LINQtoDataset application is created.
+   5. Right-click the project name (LINQtoDataset) in Solution Explorer and select the Add→New Item option from the context menu. The Add New Item dialog box appears.
+   6. Select Class in the middle pane, and enter the name Student.cs in the Name text box of the Add New Item dialog box.
+   7. Click the Add button.

Add the code given in Listing 10.12 to the Student.cs file:

Listing 10.12: Showing the Code to Add to the Student.cs File of the LINQtoDataset Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace LINQtoDataset
{
    class Student
    {
        public int Id;
        public string Name;
    }
}
```

Add the code given in Listing 10.13 to the Program.cs file of the LINQtoDataset application:

Listing 10.13: Adding Code to the Program.cs File of the LINQtoDataset Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Data;
namespace LINQtoDataset
{
    class Program
    {
        static DataTable GetDataTable(Student[] students)
        {
            DataTable table = new DataTable();
            table.Columns.Add("Id", typeof(Int32));
            table.Columns.Add("Name", typeof(string));
            foreach (Student s in students)
            {
```