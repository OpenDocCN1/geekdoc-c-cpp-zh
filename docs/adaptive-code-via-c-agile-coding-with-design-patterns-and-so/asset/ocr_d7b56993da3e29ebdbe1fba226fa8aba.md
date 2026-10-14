IDisposable. Extending the IDisposable interface burdens all implementations with the requirement that they implement a Dispose method, even in circumstances where this is unnecessary. Instead, IDisposable should be treated as an implementation detail and assigned to classes on an individual basis. This then leads naturally to the application of the Responsible Owner pattern and the Factory Isolation pattern.

The examples so far have all targeted the lifetime of the IDbConnection interface. Unfortunately, this interface extends the IDisposable interface. If, instead, the assumption is made that the target interface does not extend IDisposable, the client-side view of the Factory Isolation pattern would look like the code in Listing 9-18.

# LISTING 9-18 An example of a client using the Factory Isolation pattern.

Click here to view code image

```
public IEnumerable<TaskDto> GetAllTasks()
{
    var allTasks = new List<TaskDto>();
    connectionFactory.With(connection =>
    {
        connection.Open();
        using (var transaction = connection.BeginTransaction())
        {
            var command = connection.CreateCommand();
            command.Transaction = transaction;
            command.CommandType = CommandType.StoredProcedure;
            command.CommandText = "[dbo].[get_all_tasks]";
            using (var reader = command.ExecuteReader(CommandBehavior.CloseConnection))
            {
                while (reader.Read())
                {
                    allTasks.Add(
                        new TaskDto
                        {
                            ID = reader.GetInt32(IDIndex),
                            Description = reader.GetString(DescriptionIndex),
                            Priority = reader.GetString(PriorityIndex),
                            DueDate = reader.GetDateTime(DueDateIndex),
                            Completed = reader.GetBoolean(CompletedIndex)
                        }
                    );
                }
            }
        }
    });
```