```
return allTasks;
}
}
```

Note that the return value from the CreateConnection method is being disposed by the using block. This is viable in this instance, because the product from the factory implements IDisposable. Through interface inheritance, it is possible to enforce multiple interfaces on implementors.

However, the question must be asked whether every implementation will definitely need every interface. Sometimes they do, but given the wide variety of implementations that an interface can have—long after it was originally written—it is a big assumption to make. When it comes to IDisposable, I’m not sure it always applies.

# The Responsible Owner pattern

Instead of artificially forcing the IDisposable interface onto every implementation, you can use it only on those that truly need it. This does cause a problem, though. If the product of the factory—your interface—does not implement IDisposable, you can no longer use a using block to neatly dispose of the product after it falls out of scope. In this case, you must use the Responsible Owner pattern.

Listing 9-17 shows that the using block can be replaced with a try/finally block, and that you can check at run time to find out whether the product implements the IDisposable interface.

# LISTING 9-17 The Responsible Owner pattern ensures that resources are disposed of appropriately.

Click here to view code image

```
public IEnumerable<TaskDto> GetAllTasks()
{
    var allTasks = new List<TaskDto>();

    var connection = connectionFactory.CreateConnection();
    try
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
```