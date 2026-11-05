```
if (dtModifiedRows != null)
{
    for (int i = 0; i < dtModifiedRows.Rows.Count; i++)
    {
        dtModifiedRows.Rows[i]["RowState"] = 16;
    }
}

// For inserted rows set RowState = 4
if (dtAddedRows != null)
{
    for (int i = 0; i < dtAddedRows.Rows.Count; i++)
    {
        dtAddedRows.Rows[i]["RowState"] = 4;
    }
}

try
{
    //Update Database
    if (dtAddedRows != null)
    {
        adapter.Update(dtAddedRows);
    }
    if (dtDeletedRows != null)
    {
        adapter.Update(dtDeletedRows);
    }
    if (dtModifiedRows != null)
    {
        adapter.Update(dtModifiedRows);
    }
}
catch (Exception exception)
{
}
```

# Step 4 - The complete Data Access Layer code using the above function.

ConnString is the name of connection string in configuration file.

```
public class DataAccessLayer
{
    SqlConnection connection;
    SqlCommand command;
    SqlDataAdapter adapter;
}
```