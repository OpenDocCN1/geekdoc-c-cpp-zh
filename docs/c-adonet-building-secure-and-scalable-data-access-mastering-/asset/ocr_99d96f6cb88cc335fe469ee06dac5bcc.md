```
DataRow row = dataTable.NewRow();
row["EmployeeID"] = 101;
row["EmployeeName"] = "John Doe";
dataTable.Rows.Add(row);
```

# Accessing Data in a DataTable

You can access data in a DataTable using the Rows property. Here's an example:

```
foreach (DataRow row in dataTable.Rows)
{
    Console.WriteLine("Employee ID: {0}, Employee Name: {1}", row["EmployeeID"], row["EmployeeName"]);
}
```

# Updating Data in a DataTable

You can update data in a DataTable using the Rows property. Here's an example:

```
foreach (DataRow row in dataTable.Rows)
{
    row["EmployeeName"] = "John Smith";
}
```

# Deleting Data from a DataTable

You can delete data from a DataTable using the Rows property. Here's an example:

```
foreach (DataRow row in dataTable.Rows)
{
    row.Delete();
}
```