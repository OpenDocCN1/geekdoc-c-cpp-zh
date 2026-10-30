```
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
            });
    }
}

return allTasks;
}
```

The first change is made to the entry point, where an injection factory is used for constructing the service. This is a lambda expression that has access to the container for resolving parameters and returns a new instance of the service. The call to the ISettings service's GetSettings method has been moved to this injection factory to retrieve the connection string. This is passed to the SqlConnection constructor which, in turn, is passed to the service.

In the GetAllTasks() method, the presence of the using(connection) is problematic. This ensures that SqlConnection.Dispose() is called at the end of the using scope. After this call, the connection can no longer be used, yet you could feasibly call this method again.

Instead, what if the TaskServiceAdo implemented IDisposable and delegated its Dispose method to that of the connection? This is explored in Listing 12-14.

# LISTING 12-14 The service implements IDisposable so that it can dispose of the connection.

```
public class TaskServiceAdo : ITaskService, IDisposable
{
    public TaskServiceAdo(IDbConnection connection)
    {
        this.connection = connection;
    }

    public IEnumerable<TaskDto> GetAllTasks()
```