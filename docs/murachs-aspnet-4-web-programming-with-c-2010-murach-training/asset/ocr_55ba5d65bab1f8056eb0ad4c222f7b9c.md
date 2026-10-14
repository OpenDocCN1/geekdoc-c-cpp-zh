# Allowable return types for a select method

| Return type | Description |
|---|---|
| IEnumerable | A collection such as an ArrayList or HashTable or a strongly-typed collection such as System.Collections.Generic.List. (Because the DataReader and DataView classes implement IEnumerable, the select method can also return a data reader or a data view.) |
| DataTable | If the select method returns a data table, the ObjectDataSource control automatically extracts a data view from the table and uses the view for data binding. |
| DataSet | If the select method returns a dataset, the ObjectDataSource control extracts a data view from the first data table in the dataset and uses the view for data binding. |
| Object | If the select method returns an object, the ObjectDataSource control wraps the object in an IEnumerable collection with just one item, then does the data binding as if the method returned an IEnumerable object. |

# A select method that returns a data reader

```
public static IEnumerable GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlCommand cmd = new SqlCommand(sel, con);
    con.Open();
    SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
    return dr;
}
```

# A select method that returns a dataset

```
public static DataSet GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlDataAdapter da = new SqlDataAdapter(sel, con);
    DataSet ds = new DataSet();
    da.Fill(ds, "Categories");
    return ds;
}
```

# Description

+   - The select method returns data retrieved from the underlying database. It can return the data in several forms, including a data reader or a dataset.
+   - If the select method returns a dataset, the object data source can cache the data.
+   - The select method can also return a strongly-typed collection using C#’s generics feature. See figure 17-15 for an example.
+   - If the select method accepts parameters, the parameters must be declared within the SelectParameters element of the ObjectDataSource control. Within this element, you can use the ControlParameter element to declare a parameter that’s bound to another control on the page.