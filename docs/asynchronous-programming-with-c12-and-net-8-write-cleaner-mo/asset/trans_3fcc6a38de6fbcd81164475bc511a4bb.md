
```csharp
{
    foreach (var innerEx in ex.InnerExceptions)
    {
        Console.WriteLine($"Inner Exception: {innerEx.Message}");
    }
    // Handle or log aggregate exceptions
}
}
```

处理异常和错误场景在异步代码中至关重要，对于构建健壮可靠的应用程序至关重要。通过遵循诸如适当的异常传播、处理预期异常、使用 `try/catch` 块、处理任务组合、记录错误和报告问题等最佳实践，开发人员可以确保异步代码可预测地运行并优雅地处理错误。了解异步操作、任务和 await 点如何与异常处理机制交互，有助于在 C# 12 和 .NET 8 中设计具有弹性的异步代码库。将这些实践纳入你的异步编程工作流程，以增强代码质量、错误处理和整体应用程序稳定性。

## 第 11 章：设计结构良好的异步 API 和模式

### 为创建结构良好且高效的异步 API 建立最佳实践

为 C# 12 和 .NET 8 建立创建结构良好且高效的异步 API 的最佳实践，对于开发可扩展、响应迅速且可维护的应用程序至关重要。异步 API 利用 async/await 模式的强大功能，高效地处理 I/O 绑定操作、并行处理和长时间运行的任务。在本次探讨中，我们将讨论设计结构良好且高效的异步 API 的关键最佳实践、模式和代码示例。

### 1. 遵循命名约定：

遵循异步方法的标准命名约定以表明其异步特性。为异步方法使用 `Async` 后缀以使其用途清晰。

```csharp
public async Task<int> GetDataAsync(int id)
{
    // Asynchronous logic here
}
```

### 2. 异步 API 的设计原则：

- **单一职责原则 (SRP)：** 遵循 SRP 以确保异步方法具有清晰且集中的目的。避免在同一方法中混合同步和异步逻辑。

```csharp
public async Task<int> GetDataAsync(int id)
{
    // Asynchronous logic to fetch data
}

public async Task ProcessDataAsync(int id)
{
    // Asynchronous logic to process data
}
```

- **接口隔离原则 (ISP)：** 设计遵循 ISP 的接口，在需要时将方法的同步和异步版本分离，以为 API 的使用者提供灵活性和清晰度。

```csharp
public interface IDataService
{
    Task<int> GetDataAsync(int id);
}

public class DataService : IDataService
{
    public async Task<int> GetDataAsync(int id)
    {
        // Asynchronous implementation
    }
}
```

### 3. 返回 Task 或 ValueTask：

根据异步操作的复杂性和性能要求考虑返回 `Task<T>` 或 `ValueTask<T>`。对于简单且频繁执行的运算，使用 `ValueTask<T>` 以避免不必要的分配。

```csharp
public async Task<int> GetDataAsync(int id)
{
    await Task.Delay(100); // Simulated async operation
    return id * 10;
}
```

### 4. 使用 Async/Await 模式：

在整个 API 中始终遵循 async/await 模式以利用非阻塞 I/O 和并发。使用 `await` 关键字与异步方法一起用于异步操作。

```csharp
public async Task<int> MultiplyAsync(int a, int b)
{
    await Task.Delay(100); // Simulated async operation
    return a * b;
}
```

### 5. 适当处理异常：

在异步方法内处理异常，如果无法在本地处理，则使用 `throw` 传播它们。考虑将异常包装在有意义的自定义异常中以获得更好的错误处理。

```csharp
public async Task<int> DivideAsync(int dividend, int divisor)
{
    try
    {
        await Task.Delay(100); // Simulated async operation
        return dividend / divisor;
    }
    catch (DivideByZeroException ex)
    {
        throw new ArgumentException("Invalid divisor.", ex);
    }
}
```

### 6. 提供取消支持：

通过在异步方法中接受 `CancellationToken` 参数来支持取消，以便使用者可以取消长时间运行的操作。

```csharp
public async Task<int> ProcessDataAsync(int id,
    CancellationToken cancellationToken = default)
{
    await Task.Delay(1000, cancellationToken); // Simulated long-running operation
    return id;
}
```

### 7. 避免阻塞调用：

避免在异步方法中使用 `Task.Result`、`Task.Wait` 或同步 API 等阻塞调用，因为它们可能导致死锁并降低性能。

```csharp
public async Task<int> GetDataAsync(int id)
{
    // Avoid blocking calls like Task.Result or synchronous APIs here
    await Task.Delay(100); // Simulated async operation
    return id * 10;
}
```

### 8. 使用异步初始化：

对于需要异步初始化的类型，使用异步构造函数或工厂方法进行异步初始化。

```csharp
public class DataService
{
    private readonly HttpClient _httpClient;

    public DataService()
    {
        _httpClient = new HttpClient();
    }

    public async Task InitializeAsync()
    {
        await SomeInitializationAsync();
    }

    private async Task SomeInitializationAsync()
    {
        // Perform async initialization tasks
    }
}
```

### 9. 提供清晰的文档：

使用 XML 注释或文档清晰地记录异步 API，以解释异步方法的用途、参数、返回类型、异常和用法指南。

```csharp
/// <summary>
/// Retrieves data asynchronously based on the provided ID.
/// </summary>
/// <param name="id">The ID of the data to retrieve.</param>
/// <returns>A Task representing the asynchronous operation that returns the retrieved data.</returns>
public async Task<int> GetDataAsync(int id)
{
    // Asynchronous logic to fetch data
}
```

### 10. 彻底测试异步 API：

利用常见的异步设计模式对于在 C# 12 和 .NET 8 中编写清晰、可维护且高效的代码至关重要。异步设计模式帮助开发人员管理并发、提高响应能力并以结构化的方式组织代码。在本次探讨中，我们将讨论两种常见的异步设计模式：生产者-消费者模式和事件驱动模式。我们将提供解释、示例和代码片段，以演示它们在异步编程中的实现和优势。

### 1. 生产者-消费者模式：

生产者-消费者模式在异步编程中被广泛使用，用于将数据的生成（生产者）与其消费（消费者）分离。当处理异步数据处理、并行性和资源共享时，此模式很有用。

### 关键组件：

- **生产者**：异步生成或生产数据。
- **消费者**：异步消费或处理数据。
- **缓冲区/队列**：生产者将数据存储以供消费者消费的共享数据结构。

### 示例实现：

```csharp
public class ProducerConsumerExample
{
    private readonly Queue<int> _queue = new Queue<int>();
    private readonly object _lock = new object();

    public void StartProducer()
    {
        Task.Run(async () =>
        {
            while (true)
            {
                await Task.Delay(1000); // Simulate data generation delay
                int data = GenerateData();
                EnqueueData(data);
            }
        });
    }

    public void StartConsumer()
    {
        Task.Run(async () =>
        {
            while (true)
            {
                await Task.Delay(2000); // Simulate data consumption delay
                int data = DequeueData();
                ProcessData(data);
            }
        });
    }

    private int GenerateData()
    {
        return new Random().Next(1, 100);
    }

    private void EnqueueData(int data)
    {
        lock (_lock)
        {
```
