Analyzer, or run the StoredProcs.sql file that is part of the downloadable code for this chapter. This file installs each of the stored procedures in this section:

```
```sql
CREATE PROCEDURE RegionUpdate (@RegionID INTEGER,
    @RegionDescription NCHAR (50) ) AS
SET NOCOUNT OFF
UPDATE Region
    SET RegionDescription = @RegionDescription
    WHERE RegionID = @RegionID
GO
```
```

code download StoredProcs.sql

An update command on a more real-world table might need to reselect and return the updated record in its entirety. This stored procedure takes two input parameters (@RegionID and @RegionDescription), and issues an UPDATE statement against the database.

To run this stored procedure from within .NET code, you need to define a SQL command and execute it:

```
```csharp
SqlCommand cmd = new SqlCommand("RegionUpdate", conn);
cmd.CommandType = CommandType.StoredProcedure;
cmd.Parameters.AddWithValue ( "@RegionID", 23 );
cmd.Parameters.AddWithValue ( "@RegionDescription", "Something" );
```
```

code download StoredProcs.sql

This code creates a new SqlCommand object named aCommand, and defines it as a stored procedure. You then add each parameter in turn, using the AddWithValue method. This constructs a parameter and also sets its value — you can also manually construct SqlParameter instances and add these to the Parameters collection if appropriate.

The stored procedure takes two parameters: the unique primary key of the Region record being updated and the new description to be given to this record. After the command has been created, it can be executed by issuing the following command:

```
```csharp
cmd.ExecuteNonQuery();
```
```

Because the procedure returns nothing, ExecuteNonQuery() will suffice. Command parameters can be set directly, using the AddWithValue() method, or by constructing SqlParameter instances. Note that the parameter collection is indexable by position or parameter name.

# Record Deletion

The next stored procedure required is one that can be used to delete a Region record from the database:

```
```sql
CREATE PROCEDURE RegionDelete (@RegionID INTEGER) AS
SET NOCOUNT OFF
DELETE FROM Region
WHERE        RegionID = @RegionID
GO
```
```

code download StoredProcs.sql

This procedure requires only the primary key value of the record. The code uses a SqlCommand object to call this stored procedure as follows:

```
```csharp
SqlCommand cmd = new SqlCommand("RegionDelete", conn);
cmd.CommandType = CommandType.StoredProcedure;
cmd.Parameters.Add(new SqlParameter("@RegionID", SqlDbType.Int, 0,
    "RegionID"));
cmd.UpdatedRowSource = UpdateRowSource.None;
```
```

code download StoredProcs.cs