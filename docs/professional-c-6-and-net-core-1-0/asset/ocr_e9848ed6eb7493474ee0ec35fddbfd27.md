Compared to the time it costs to make a service call, the additional time needed to access the indexer can be ignored:

```
```csharp
int id = (int)reader["ProductID"];
string name = (string)reader["Name"];
DateTime from = (DateTime)reader["StartDate"];
DateTime? to = (DateTime?)reader["EndDate"];
```
```

# Calling Stored Procedures

Calling a stored procedure with a command object is just a matter of defining the name of the stored procedure, adding a definition for each parameter of the procedure, and then executing the command with one of the methods presented in the previous section.

The following sample calls the stored procedure `uspGetEmployeeManagers` to get all the managers of an employee. This stored procedure receives one parameter to return records of all managers using recursive queries:

```
```sql
CREATE PROCEDURE [dbo].[uspGetEmployeeManagers]
    @BusinessEntityID [int]
AS
—...
```
```

To see the implementation of the stored procedure, check the AdventureWorks2014 database.

To invoke the stored procedure, the `CommandText` of the `SqlCommand` object is set to the name of the stored procedure, and the `CommandType` is set to `CommandType.StoredProcedure`. Other than that, the command is invoked similarly to the way you’ve seen before. The parameter is created using the `CreateParameter` method of the `SqlCommand` object, but you can use other methods to create the parameter used earlier as well. With the parameter, the `SqlDbType`, `ParameterName`, and `Value` properties are filled. Because the stored procedure returns records, it is invoked by calling the method `ExecuteReader` (code file `CommandSamples/Program.cs`):

```
```csharp
private static void StoredProcedure(int entityId)
{
    using (var connection = new SqlConnection(GetConnectionString()))
    {
        SqlCommand command = connection.CreateCommand();
        command.CommandText = "[dbo].[uspGetEmployeeManagers]";
        command.CommandType = CommandType.StoredProcedure;
        SqlParameter p1 = command.CreateParameter();
        p1.SqlDbType = SqlDbType.Int;
        p1.ParameterName = "@BusinessEntityID";
        p1.Value = entityId;
        command.Parameters.Add(p1);
        connection.Open();
        using (SqlDataReader reader = command.ExecuteReader())
        {
            while (reader.Read())
            {
                int recursionLevel = (int)reader["RecursionLevel"];
```
```