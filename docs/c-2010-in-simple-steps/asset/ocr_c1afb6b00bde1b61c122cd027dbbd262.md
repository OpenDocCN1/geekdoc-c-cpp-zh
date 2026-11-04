```
table.Rows.Add(s.Id, s.Name);
}
return (table);
}
static void OutputDataTableHeader(DataTable dt, int Columnwidth)
{
    string format = string.Format("{0:0,-1}{2}", "{", Columnwidth, "}");
    foreach (DataColumn c in dt.Columns)
    {
        Console.Write(format, c.ColumnName);
    }
    Console.WriteLine();
    foreach (DataColumn c in dt.Columns)
    {
        for (int i = 0; i < Columnwidth; i++)
        {
            Console.Write("=");
        }
    }
    Console.WriteLine();
}
static void Main(string[] args)
{
Student[] students = {
    new Student {Id = 1, Name = "A"},
    new Student {Id = 2, Name = "B"},
    new Student {Id = 3, Name = "C"},
    new Student {Id = 4, Name = "D"},
    new Student {Id = 5, Name = "E"},
    new Student {Id = 6, Name = "F"}
};
DataTable dt = GetDataTable(students);
Console.WriteLine("{0}Result{0}", System.Environment.NewLine);
OutputDataTableHeader(dt, 15);
foreach (DataRow dr in dt.Rows)
{
    Console.WriteLine("{0,-15}{1,-15}",
        dr.Field<int>(0),
        dr.Field<string>(1));
}
Console.ReadLine();
}
}
```

In Listing 10.13, a set of student names is displayed in a tabular format. The tables and columns are created in the code with the help of the DataTable class.

Press the F5 key to run the application. The output appears, as shown in Fig.C# 10.17:

![](bbox=[0.26, 0.6, 0.67, 0.75])

Fig.C# 10.17

In Fig.C# 10.17, you can see that the Id and Name properties of the students are displayed in a tabular format. Let's now discuss a new feature that has been introduced in LINQ with .NET Framework 4.0. This new feature is known as Parallel LINQ or PLINQ.