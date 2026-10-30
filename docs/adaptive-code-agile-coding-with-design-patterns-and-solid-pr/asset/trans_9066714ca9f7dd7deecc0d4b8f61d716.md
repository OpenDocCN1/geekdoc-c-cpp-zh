

与其在方法中释放连接，连接只会在服务被释放时才被释放。这就引出了一个重要问题：任务服务应该在何时被释放？所有接收 `ITaskService` 作为构造函数参数的任务客户端是否也应该实现 `IDisposable`？谁来释放这些对象？最终，你需要在某个地方调用 `Dispose()`。

需要注意的是，如果一个类通过构造函数接收到一个依赖，它就不应该手动释放该依赖本身。该类无法保证它获得的是该依赖的唯一实例；它可能与其他类共享，因此在不给其他类带来负面影响的情况下无法释放它。

关于在使用依赖注入时如何管理对象生命周期的答案，更接近于服务最初的实现方式。

## 连接工厂

工厂模式是一种用委托给专门用于创建对象的类来替代手动对象实例化的方式。

连接工厂可能看起来像列表 12-15 中所示的接口。该接口通过返回 `IDbConnection` 接口而不是将所有客户端绑定到 `SqlConnection` 类而变得稍微更通用。

**LISTING 12-15** 连接工厂接口非常简单。

```csharp
public interface IConnectionFactory
{
    IDbConnection CreateConnection();
}
```

该接口将被注入到任务服务中，以便你可以在不手动构造连接的情况下获取连接，同时通过模拟保持服务的测试性。列表 12-16 显示了重构后的服务。

**LISTING 12-16** 依赖注入可以与工厂模式协同工作。

```csharp
public class TaskServiceAdo : ITaskService
{
    private readonly IConnectionFactory connectionFactory;

    public TaskServiceAdo(IConnectionFactory connectionFactory)
    {
        this.connectionFactory = connectionFactory;
    }

    public IEnumerable<TaskDto> GetAllTasks()
    {
        var allTasks = new List<TaskDto>();

        using(var connection = connectionFactory.CreateConnection())
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
                            });
                    }
                }
            }

            return allTasks;
        }
    }
}
```

请注意，`CreateConnection` 方法的返回值正由 `using` 块释放。在此实例中这是可行的，因为工厂的产品实现了 `IDisposable`。通过接口继承，可以强制实现者在多个接口上实现。

然而，必须问这样一个问题：是否每个实现都需要每个接口？有时需要，但鉴于接口在最初编写后很长时间内可能具有的各种实现，这是一个很大的假设。至于 `IDisposable`，我不确定它是否总是适用。

## 责任所有者模式

与其人为地强制所有实现都实现 `IDisposable` 接口，你只能在真正需要时使用它。这确实会带来一个问题。如果工厂的产品——你的接口——没有实现 `IDisposable`，你就不能再使用 `using` 块在产品超出作用域后整洁地释放它。在这种情况下，你必须使用责任所有者模式。

列表 12-17 显示 `using` 块可以用 `try/finally` 块替换，并且你可以在运行时检查产品是否实现了 `IDisposable` 接口。

**LISTING 12-17** 责任所有者模式确保资源得到适当释放。

```csharp
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
            command.CommandText = "[dbo].[Get_all_tasks]";

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
    }
    finally
    {
        if (connection is IDisposable)
        {
            var disposableConnection = connection as IDisposable;
            disposableConnection.Dispose();
        }
    }

    return allTasks;
}
```

只有当连接是 `IDisposable` 类型时，你才会尝试在其上调用 `Dispose` 方法。这无论工厂返回的产品是否实现 `IDisposable` 都能工作，但如果实现了，它将通过释放来清理其资源。

责任所有者模式会确定性地释放实现 `IDisposable` 的对象。该模式有效地忽略了未实现 `IDisposable` 的对象。然而，SOLID 代码通常会导致多个装饰器相互包装以添加额外功能。在这种情况下，只有当顶层对象实现 `IDisposable` 时，责任所有者模式才能正确发挥作用。当外部装饰器未实现 `IDisposable`，但后续层实现了时，责任所有者模式将无法正确释放这些实例。相反，你可以使用工厂隔离模式。

## 工厂隔离模式

该模式能够确定性地释放 SOLID 代码经常形成的复杂对象图。它以实验室中常见的手套箱隔离器命名。这些是带集成手套的玻璃或金属箱，可安全受保护地访问内容物。类似地，工厂隔离模式允许安全受保护地访问一个对象实例，并在使用后正确释放它。

工厂隔离模式仅在目标接口未实现 `IDisposable` 时才需要。扩展 `IDisposable` 接口会给所有实现带来实现 `Dispose` 方法的要求，即使在不必要的情况下也是如此。相反，`IDisposable` 应被视为实现细节，并仅逐个分配给类。这导致了责任所有者模式和工厂隔离模式的应用。

到目前为止的示例都针对 `IDbConnection` 接口的生命周期。不幸的是，该接口扩展了 `IDisposable` 接口。如果相反假设目标接口不扩展 `IDisposable`，客户端对工厂隔离模式的视图将看起来像列表 12-18 中的代码。

**LISTING 12-18** 客户端使用工厂隔离模式的示例。

```csharp
public IEnumerable<TaskDto> GetAllTasks()
{
    var allTasks = new List<TaskDto>();
    connectionFactory.WithConnection(connection =>
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

    return allTasks;
}
```

