InfoMessage and StateChange events. The InfoMessage event is fired every time an information or warning message is returned from SQL Server. The StateChange event is fired when the state of the connection changes—for example, the connection is opened or closed (code file ConnectionSamples/Program.cs):

```
public static void ConnectionInformation()
{
    using (var connection = new
SqlConnection(GetConnectionString()))
    {
        connection.InfoMessage += (sender, e) =>
        {
            WriteLine($"warning or info {e.Message}");
        };
        connection.StateChange += (sender, e) =>
        {
            WriteLine($"current state: {e.CurrentState}, before:
{e.OriginalState}");
        };
        connection.Open();

        WriteLine("connection opened");
        // Do something useful
    }
}
```

When you run the application, you can see the StateChange event fired and the Open and Closed state:

```
current state: Open, before: Closed
connection opened
current state: Closed, before: Open
```

# Commands

The “Using Database Connections” section briefly touched on the idea of issuing commands against a database. A command is, in its simplest form, a string of text containing SQL statements to be issued to the database. A command could also be a stored procedure, shown later in this section.

A command can be constructed by passing the SQL statement as a parameter to the constructor of the Command class, as shown in this example (code file CommandSamples/Program.cs):

```
public static void CreateCommand()
{
    using (var connection = new
SqlConnection(GetConnectionString()))
    {
        string sql ="SELECT BusinessEntityID, FirstName, MiddleName,
LastName" +
            "FROM Person.Person";
        var command = new SqlCommand(sql, connection);

        connection.Open();

        // etc.

```