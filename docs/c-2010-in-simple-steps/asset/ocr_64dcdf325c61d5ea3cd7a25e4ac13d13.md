```
public int Age
{
    get;
    set;
}
public string ID
{
    get;
    set;
}
}
}
```

In Listing 7.14, a class named Student, is added to the MainWindow.xaml file of the DataGridDemo application.

The Student class contains three private data members, id, name and age. Three properties, ID, Name and Age are also defined to assign and retrieve the values of the id, name, and age data members defined in the Student class. Inside of the constructor of the partial class MainWindow, the values of the ID, Name, and Age properties of the Student class are added to the Items collection of the DataGrid control, dataGrid1, by using the following lines of code:

```
dataGrid1.Items.Add(new Student() { ID="ST01", Name = "John", Age = 14});
dataGrid1.Items.Add(new Student() { ID="ST02", Name = "Andrew", Age = 11});
dataGrid1.Items.Add(new Student() { ID="ST03", Name = "Katie", Age = 16});
```

To display the values of the ID, Name, and Age properties inside the dataGrid1 control, three columns, col1, col2, and col3 are created and bound to the ID, Name, and Age properties, respectively, by using the following lines of code:

```
DataGridTextColumn col1 = new DataGridTextColumn();
col1.Binding = new Binding("ID");
DataGridTextColumn col2 = new DataGridTextColumn();
col2.Binding = new Binding("Name");
DataGridTextColumn col3 = new DataGridTextColumn();
col3.Binding = new Binding("Age");
```

Note that DataGridTextColumn is a class that is used to display textual content inside a DataGrid control. The col1, col2, and col3 columns are then added to the dataGrid1 control, by using the following lines of code:

```
dataGrid1.Columns.Add(col1);
dataGrid1.Columns.Add(col2);
dataGrid1.Columns.Add(col3);
```

The headers for col1, col2, and col3 columns are set to clearly identify what data each of these columns is displaying in the dataGrid1 control, by using the following lines of code:

```
col1.Header = "Student_ID";
col2.Header = "Name of Student";
col3.Header = "Age of Student";
```

Press the F5 key to run the DataGridDemo application. The output appears, as shown in Fig.C+7.30: