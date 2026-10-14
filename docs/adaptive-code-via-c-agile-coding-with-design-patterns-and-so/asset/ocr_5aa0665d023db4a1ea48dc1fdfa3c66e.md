```
}

public void Dispose()
{
    connection.Dispose();
}
}
```

Instead of disposing the connection in the method, the connection is disposed of only when the service is disposed. This raises the important question of when the task service should be disposed. Should all of the task’s clients, which will receive ITaskService as a constructor parameter, also implement IDisposable? Who will dispose of these objects? Eventually, you would need to call Dispose() on something.

It is important to note that if a class is handed a dependency via its constructor, *it should not manually dispose of the dependency itself*. The class cannot guarantee that it has been given the one and only instance of the dependency; it might share it with others and therefore cannot dispose of it without potentially having a negative impact on other classes.

The answer to the question of how to manage the lifetime of objects when using dependency injection is much closer to how the service was originally implemented.

# The connection factory

Recall that the Factory pattern is a way of replacing manual object instantiation with delegation to a class whose purpose is to create objects.

A connection factory could look something like the interface shown in Listing 9-15. This interface has been made slightly more general by returning the IDbConnection interface, rather than committing all of its clients to the SqlConnection class.

# LISTING 9-15 The connection factory interface is very simple.

Click here to view code image

```
public interface IConnectionFactory
{
    IDbConnection CreateConnection();
}
```

This interface will be injected into the task service so that you have a way of retrieving a connection without manually constructing it, keeping the service testable through mocking. Listing 9-16 shows the refactored service.

# LISTING 9-16 Dependency injection can work in tandem with the Factory pattern.