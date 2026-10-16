

使用 Entity Framework 的异步 Get 仓储操作可能如下所示：

```
public class EFClientRepository
{
    public async Task<Option<Client>> GetByIdAsync(int id)
    {
        using (var context = new DbContext())
        {
            var clients = await context.Clients.ToListAsync();
            Option<Client> client = clients.SingleOrDefault(x => x.Id == id);
            return client;
        }
    }
}
```

或者在领域驱动或微服务环境中，使用 HttpClient 的异步操作从另一个服务获取 Client：

```
public class HttpClientRepository
{
    public async Task<Option<Client>> GetByIdAsync(int id)
    {
        HttpClient httpClient = new HttpClient();
        HttpClient response = await httpClient.GetAsync("");

        if (response.IsSuccessStatusCode)
        {
            var streamTask = httpClient.GetStreamAsync($"https://myapi/client/{id}");
            var client = await JsonSerializer.DeserializeAsync<Client>(await streamTask);
            return Some(client);
        }
        else
        {
            return None;
        }
    }
}
```

为了模拟一般情况，我们将使用这个模拟的 MockClientRepository：

```
public class MockClientRepository
{
    List<Client> clients = new List<Client>{
        new Client{Id=1, Name="Jim" },
        new Client{Id=2, Name="John" }
```

```
public Task<Option<Client>> GetByIdAsync(int id) =>
    System.Threading.Tasks.Task.Run(() =>
    {
        System.Threading.Thread.Sleep(1000);
        Option<Client> maybeClient = clients.SingleOrDefault(x => x.Id == id);
        return maybeClient;
    });
```

这里重要的一点是，我们有一个 Get 方法签名：

```
OptionAsync<Client> GetByIdAsync(int id)
```

我们现在可以组合出 GetNameByIdAsync：

```
public class Controller
{
    MockClientRepository clients = new MockClientRepository();

    public Task<string> GetNameByIdAsync(int clientId) =>
        clients
            .GetByIdAsync(clientId)
            .Map(x => x.Map(client => client.Name))
            .Match(Some: (name) => name,
                   None: () => "no client");
}
```

```
var assignedEmployeeName = await new Controller().GetNameByIdAsync(1);
```

这里我们使用了复合的 Map 来绕过 Task，并使用内部 Option 的 Map：

```
.Map(x => x.Map(client => client.Name))
```

幸运的是，language-ext 几乎为每一种类型都提供了 MapT。因此，我们可以改用这个：

```
public class Controller
{
    MockClientRepository clients = new MockClientRepository();

    public Task<string> GetNameByIdAsync(int clientId) =>
        clients
            .GetByIdAsync(clientId)
```

```
.MapT(client => client.Name)
.Match(Some: (name) => name,
    None: () => "no client");
}
```

## 附注：

在本例中，language-ext 确实为我们提供了一个扩展方法，用于在包含 Option 的 Task 上执行 Match：

```
public static Task<B> Match<A, B>(this Task<Option<A>> self, Func<A, B> Some, Func<B> None)
```

```
public static OptionAsync<B> MapAsync<A, B>(this Task<Option<A>> self, Func<A, B> f);
public static Task<B> Match<A, B>(this Task<Option<A>> self, Func<A, B> Some, Func<B> None);
public static Task<Unit> Match<A>(this Task<Option<A>> self, Action<A> Some, Action None);
public static Task<B> MatchAsync<A, B>(this Task<Option<A>> self, Func<A, Task<B>> Some, Func<Task<B>> None);
public static Task<B> MatchAsync<A, B>(this Task<Option<A>> self, Func<A, B> Some, Func<Task<B>> None);
```

尽管如此，在接下来的章节中我们将会看到，Task<Either<,>> 没有对应的 Match 扩展方法。

## 4.14 组合 Task 和 Option – OptionAsync<T>

OptionAsync<T> 是看待 Task 与 Option 组合的另一种方式，它属于 Monad Transformer 的范畴。我们还没有讲到 Monad 那一章，而且本书中也不会探讨 Monad Transformer 的内部机制。但即使没有理论，它用起来也非常直观。OptionAsync<T> 只是在 Option 上叠加了一个 Task，并提供了一些有效的方法，如 Map 和 Match。

我们可以通过使用 .ToAsync() 方法将 Task<Option<Client>> 转换为 OptionAsync<Client>：

```
public OptionAsync<Client> GetByIdAsync(int id)
{
    Task<Option<Client>> r = System.Threading.Tasks.Task.Run(() =>
    {
        System.Threading.Thread.Sleep(1000);
        Option<Client> t = clients.SingleOrDefault(x => x.Id == id);
        return t;
    });
    return r.ToAsync();
}
```

当我们有一个 OptionAsync 后，就可以像往常一样使用 Map 和 Match：

```
public class Controller
{
    MockClientRepository clients = new MockClientRepository();

    public Task<string> GetNameByIdAsync(int clientId) =>
        clients
        .GetByIdAsync(clientId)
        .Map(client => client.Name)
        .Match(Some: (name) => name,
            None: () => "no client");
}
```

这里的 Match 返回的是 Task<string>。

## 4.15 组合 Task 和 Either – Task<Either<,>>

正如人们所预料的那样，如果我们想要传播错误消息而不只是返回 None，那么最终会得到 Either 位于 Task 内部的情况。我们可以再次修改 Repository，让它返回 Task<Either<string, Client>>：

```
public class MockClientRepository
{
    ...
    public Task<Either<string, Client>> GetByIdAsync(int id)
    {

    Task<Either<string, Client>> maybeClientTask =
    System.Threading.Tasks.Task.Run(() =>
    {
        System.Threading.Thread.Sleep(1000);
        Option<Client> maybeClient = clients.SingleOrDefault(x => x.Id == id);
        return maybeClient.ToEither("no Client Found");
    });
        return maybeClientTask;
    }
}
```

现在我们可以将其用在控制器中（同样有两种不同的版本，其中一种使用了 MapT）：

```
public class Controller
{
```

```
MockClientRepository clients = new MockClientRepository();
public Task<Either<string, string>> GetNameByIdAsync(int clientId)
    => clients.GetByIdAsync(clientId)
        .MapT(client => client.Name);

public Task<Either<string, string>> GetNameByIdAsync1(int clientId)
    => clients.GetByIdAsync(clientId)
        .Map(x => x.Map(client => client.Name));
}
```

然后，我们终于可以通过先 await 任务、再进行 case 分析的方式来调用它：

```
var clientName = (await new Controller().GetNameByIdAsync(3))
    .Case switch
    {
        LeftCase<string, string>(var error) => error,
        RightCase<string, string>(var name) => name,
        _ => throw new NotImplementedException(),
    };
```

await 之后，我们就只剩下 Either 了。

这等同于：

```
var clientName = await new Controller().GetNameByIdAsync(3)
    .Map(x => x.Case) switch
    {
        LeftCase<string, string>(var error) => error,
        RightCase<string, string>(var name) => name,
        _ => throw new NotImplementedException(),
    };
```

甚至还可以：

```
var clientName = (await new Controller().GetNameByIdAsync(3))
    .Match(
        Right: (name) => name,
        Left: (e) => $"error {e}");
```

这就是 Either 的 Match。

## 4.16 组合 Task 和 Either – EitherAsync<>

EitherAsync<> 是另一个 Monad Transformer，它帮助我们处理 Task 与 Either 的组合。同样，EitherAsync<> 只是在 Either 上叠加了一个 Task，并提供了一些有效的方法，如 Map 和 Match。

```
public class MockClientRepository
{
    public EitherAsync<string, Client> GetByIdAsync(int id)
    {
        Task<Either<string, Client>> maybeClientTask =
            System.Threading.Tasks.Task.Run(() =>
        {
            System.Threading.Thread.Sleep(1000);
            Option<Client> maybeClient = clients.SingleOrDefault(x => x.Id == id);
            return maybeClient.ToEither("no Client Found");
        });
        return maybeClientTask.ToAsync();
    }
}
```

与 Task<Either<>> 相比，EitherAsync 的不同之处就在于 Match：

```
public class Controller
{
    MockClientRepository clients = new MockClientRepository();
    public Task<string> GetNameByIdAsync(int clientId)
        => clients.GetByIdAsync(clientId)
            .Map(client => client.Name)
            .Match(
                Right: (name) => name,
                Left: (e) => $"error {e}");
}
```

```
var clientName = await new Controller().GetNameByIdAsync(3);
```

另一种写法是：

```
public class Controller
{
    MockClientRepository clients = new MockClientRepository();
```

