```
New row updated and new RegionID assigned by database
    1  Eastern      Unchanged
    2  Western      Unchanged
    3  Northern     Unchanged
    4  Southern     Unchanged
    5  North West   Unchanged
```

Look at the last row in the DataTable. The RegionID had been set in code to 999, but after executing the RegionInsert stored procedure, the value has been changed to 5. This is intentional — the database will often generate primary keys for you, and the updated data in the DataTable appears because the SqlCommand definition within the source code has the UpdatedRowSource property set to UpdateRowSource.OutputParameters:

```
```csharp
SqlCommand aCommand = new SqlCommand("RegionInsert", conn);
aCommand.CommandType = CommandType.StoredProcedure;
aCommand.Parameters.Add(new SqlParameter("@RegionDescription",
    SqlDbType.NChar,
    50,
    "RegionDescription"));
aCommand.Parameters.Add(new SqlParameter("@RegionID",
    SqlDbType.Int,
    0,
    ParameterDirection.Output,
    false,
    0,
    0,
    "RegionID",  // Defines the SOURCE column
    DataRowVersion.Default,
    null));
aCommand.UpdatedRowSource = UpdateRowSource.OutputParameters;
```
```

code download DataAdapter2.cs

What this means is that whenever a data adapter issues this command, the output parameters should be mapped to the source of the row, which in this instance was a row in a DataTable. The flag states what data should be updated — the stored procedure has an output parameter that is mapped to the DataRow. The column it applies to is RegionID because this is defined within the command definition.

The following table shows the values for UpdateRowSource.

| UPDATERSOURCES VALUE | DESCRIPTION |
|---|---|
| Both | A stored procedure might return output parameters and also a complete database record. Both of these data sources are used to update the source row. |
| FirstReturnedRecord | This implies that the command returns a single record, and that the contents of that record should be merged into the original source DataRow. This is useful where an INSERT statement has a number of default (or computed) columns because after an INSERT statement these need to be synchronized with the DataRow on the client. An example might be 'INSERT (columns) INTO (table) WITH (primarykey)', then 'SELECT (columns) FROM (table) WHERE (primarykey)'. The returned record would then be merged into the original row. |
| None | All data returned from the command is discarded. |
| OutputParameters | Any output parameters from the command are mapped onto the appropriate column(s) in the DataRow. |