# C# 12 和 .NET 8 异步编程：编写更简洁、更高效的异步代码，开发响应式 UI 和可扩展的 Web 服务等等！




## 引言

### 征服响应性：释放 C# 12 和 .NET 8 异步编程的强大力量

在当今瞬息万变的数字世界中，用户要求即时满足。传统的同步编程虽然熟悉，但在某些情况下会成为瓶颈，导致应用程序迟缓且无响应。想象一下用户点击按钮，然后……什么都没有。就像看着油漆干燥一样。开发人员面临关键选择：接受卡顿的应用程序，或深入异步编程的世界，这是构建真正响应且面向未来的应用程序的秘密武器。

**使用 C#12 和 .NET 8 进行异步编程** 是您掌握这一突破性范式的全面指南。忘掉枯燥的理论；本书为您提供实践技能和知识，帮助您构建以下类型的应用程序：

- **即时响应：** 提供无缝的用户体验，单击、操作和数据检索不会出现令人沮丧的延迟。
- **同时处理复杂任务：** 摆脱同步工作流的限制，利用并发高效地处理多个任务。
- **轻松扩展：** 设计能够优雅处理日益增长的工作负载的应用程序，确保在压力下保持一致的性能。

**本书不仅仅是一系列代码示例的集合。它是您成为异步编程专家的路线图。** 无论您是经验丰富的 C# 开发者，还是渴望提升编程技能的新手，您都将获得以下收获：

- **掌握最新的 C#12 功能：** 利用前沿功能如顶层语句和异步流，使异步代码更简洁、高效且流畅。
- **发挥 .NET 8 的强大功能：** 释放 .NET 8 的性能和效率增强功能，让您的应用程序比以往任何时候都运行得更快、更顺畅。
- **深入实际应用：** 超越理论，探索跨不同领域的实践示例。学习如何在用户界面、云服务、网络通信等领域实现异步编程。
- **征服高级技术：** 探索复杂的异步工作流、并发操作以及流等前沿异步功能，以应对任何编程挑战。
- **自信测试：** 了解测试异步代码的挑战，并通过确保代码质量和可靠性的有效策略来征服它们。
- **为成功而设计：** 学习打造结构良好且高效的异步 API、模式和代码的艺术，避免常见陷阱并确保可维护性。

### 以下是您将探索的精彩主题预览：

- **转变 UI 交互：** 通过实施异步 UI 编程技术，使您的应用程序感觉响应迅速且流畅。用户不再需要等待屏幕！
- **构建可扩展的 Web 应用程序：** 利用 ASP.NET Core 8 和异步功能的强大功能，创建能够在不费力的情况下处理海量流量的 Web 应用程序。
- **征服云服务：** 无缝集成 Azure 和 AWS 等云提供商，利用异步模式实现高效的无服务器函数和通信。
- **优化效率：** 识别性能瓶颈并应用优化技术，确保您的异步应用程序以峰值性能运行。

**不要只构建应用程序；构建用户喜爱的应用程序。** 本书使您能够摆脱同步编程的限制，释放 C#12 和 .NET 8 的全部潜力。随着您掌握异步编程，您将能够提供卓越的用户体验，实现更大的可扩展性，并为您的开发技能提供未来保障。





您是否准备好将自己的应用程序从迟缓变为卓越？立即订购《C# 12 与 .NET 8 异步编程》一书，开始构建像数字世界所要求的那样响应迅速且功能强大的应用程序吧！

# 第 1 章
### 理解现代应用程序中同步编程的局限性
同步编程（即任务按顺序依次执行）一直是软件开发中的传统方法。然而，随着应用程序变得越来越复杂，性能要求不断提高，同步编程也暴露出了一些局限性，这些局限性可能会阻碍效率并降低响应能力。在本节中，我们将深入探讨同步编程的约束条件，并了解 C# 12 和 .NET 8 中的异步编程如何应对这些挑战。

### 1. 阻塞特性：
同步代码执行本质上具有阻塞性，这意味着每个操作都必须等待前一个操作完成后才能继续。这会导致效率低下，尤其是在某些操作本可并发执行且彼此不依赖的场景中。

让我们用 C# 中的一个简单示例来说明这一点：

```csharp
public void SynchronousExample()
{
    // 相互阻塞的方法调用

    var result1 = Method1();
    var result2 = Method2();

    // 在两个方法都完成之后继续执行
    ProcessResults(result1, result2);
}
```

在这个同步示例中，`Method1` 和 `Method2` 按顺序被调用，导致每个方法都会阻塞执行，直到自身完成。这可能会引入延迟，降低应用程序的整体性能。

### 2. 可扩展性：
同步编程会限制可扩展性，尤其是在需要并发处理多个请求或操作的场景中。在传统的同步模型中，每个请求通常都会占用一个线程，直到其处理完成。这种方法可能导致资源耗尽，并削弱应用程序处理大量并发用户或任务的能力。

### 3. 响应性：
在面向用户的应用程序中，响应性对于提供流畅的用户体验至关重要。耗时较长的同步操作可能导致界面卡顿或无响应，给用户带来困扰。

### 4. I/O 密集型操作：
在处理 I/O 密集型操作（如文件 I/O、网络请求或数据库查询）时，同步编程可能尤其低效。这些操作往往需要等待外部资源做出响应，在此期间应用程序线程会一直处于阻塞状态，导致 CPU 周期被浪费。

## 使用 C# 12 和 .NET 8 中的异步编程解决这些局限性：
异步编程允许任务独立执行，且不阻塞主执行线程，从而解决了同步编程的局限性。在 C# 12 和 .NET 8 中，异步编程还借助异步流、简化的异步 Main 方法以及改进的错误处理等特性得到了进一步增强。

### 1. 非阻塞执行：
在 C# 中使用 async/await 关键字，开发人员可以编写不阻塞主线程的异步代码。这使得任务可以并发执行，从而提高了应用程序的响应性和可扩展性。让我们使用异步编程来重构之前的示例：

```csharp
public async Task AsynchronousExample()
{
    // 异步启动 Method1
    var task1 = Method1Async();

    // 异步启动 Method2
    var task2 = Method2Async();

    // 等待两个任务完成
    var result1 = await task1;
    var result2 = await task2;

    // 处理结果
    ProcessResults(result1, result2);
}
```

在这个更新后的示例中，`Method1Async` 和 `Method2Async` 是返回 `Task` 对象的异步方法。通过使用 `await`，我们可以异步地等待这些任务完成，而无需阻塞主线程，从而提高了应用程序的整体性能。

### 2. 更好的可扩展性：
异步编程允许应用程序处理更多并发操作而不会耗尽系统资源，从而提升了可扩展性。与同步任务相比，异步任务使用的线程更少，因此在高并发场景下更为高效。

### 3. 更强的响应性：
通过避免阻塞操作，异步编程增强了应用程序的响应性，尤其是在涉及长时间运行任务的场景中。这对于在交互式应用程序中保持流畅的用户体验至关重要。

### 4. 处理 I/O 密集型操作：
异步编程非常适合高效处理 I/O 密集型操作。通过在等待期间释放主线程，异步任务使应用程序能够更有效地利用资源，从而提高整体吞吐量。

## C# 12 和 .NET 8 中的其他特性：
- 1. **异步流：** 异步流允许对数据集合进行异步迭代。这对于数据检索涉及异步操作（如查询数据库或使用 Web API）的场景尤为有用。

```csharp
public async IAsyncEnumerable<int> GetNumbersAsync()
{
    for (int i = 0; i < 10; i++)
    {
        await Task.Delay(100); // 模拟异步操作
        yield return i;
    }
}
```

- 2. **简化的异步 Main：** C# 12 引入了简化的异步 Main 方法，使编写控制台应用程序和其他场景的异步入口点变得更加容易。

```csharp
public static async Task Main(string[] args)
{
    await DoAsyncWork();
}
```

### 3. 改进的错误处理：
C# 12 和 .NET 8 中的异步编程改进了错误处理功能，使异常在异步代码中的传播和处理更加容易。

```csharp
public async Task ProcessDataAsync()
{
    try
    {
        await DoSomethingAsync();
    }
    catch (Exception ex)
    {
        // 处理异常
        Console.WriteLine($"错误：{ex.Message}");
    }
}
```

C# 12 和 .NET 8 中的异步编程提供了强大的工具，帮助克服现代应用程序中同步编程的局限性。通过利用非阻塞执行、更好的可扩展性、更强的响应性以及高效处理 I/O 密集型操作的能力，开发人员可以构建高性能、响应迅速的软件系统，满足当今计算环境的需求。

## 异步编程的优势：改进的响应性、可扩展性和性能
异步编程在现代软件开发中变得越来越重要，因为它能够提高响应性、可扩展性和整体性能。在本节中，我们将探讨使用 C# 12 和 .NET 8 进行异步编程的优势，并辅以代码示例来说明这些好处。

### 1. 改进的响应性：
异步编程的一个关键优势是提高了响应性，尤其是在面向用户的应用程序中。通过避免阻塞操作，异步代码允许主线程在后台任务并发执行的同时，保持对用户交互的响应。这对于创建流畅、交互式的用户体验至关重要。

让我们考虑这样一个场景：一个 Web 应用程序需要从外部 API 获取数据，同时又不希望冻结界面：

更少的线程数量。这降低了资源消耗，并提高了应用程序处理更多并发请求或任务的能力。

我们用一个并发处理多个文件的示例来说明这一点：

```csharp
public async Task ProcessFilesAsync(IEnumerable<string> fileUrls)
{
    var tasks = new List<Task>();
    foreach (var fileUrl in fileUrls)
    {
        tasks.Add(ProcessFileAsync(fileUrl));
    }

    // 等待所有任务完成
    await Task.WhenAll(tasks);
}

public async Task ProcessFileAsync(string fileUrl)
{
    // 异步下载并处理文件
    var fileData = await DownloadFileAsync(fileUrl);
    ProcessData(fileData);
}
```




在此示例中，`ProcessFilesAsync` 方法通过对每个文件 URL 异步调用 `ProcessFileAsync` 方法来并发处理多个文件。`Task.WhenAll` 的使用确保该方法等待所有文件处理任务异步完成。这种方法优化了资源利用率，并在处理大量文件时提高了应用程序的可扩展性。

## 3. 性能提升：

异步编程可以在各种场景下带来性能提升，尤其是在处理 I/O 密集型或 CPU 密集型操作时。通过允许任务并发运行并高效利用资源，异步代码可以减少整体执行时间并提高吞吐量。

考虑一个使用异步任务进行并行处理的示例：

```csharp
public async Task<int>
CalculateSumAsync(IEnumerable<int> numbers)
{
    var tasks = numbers.Select(async num =>
    {
        // Simulate CPU-bound operation asynchronously
        await Task.Delay(100);
        return num;
    });
    var results = await Task.WhenAll(tasks);
    return results.Sum();
}
```

在此示例中，`CalculateSumAsync` 方法通过利用 `Task.WhenAll` 为每个数字并行运行 CPU 密集型操作（使用 `Task.Delay` 模拟）来异步计算数字的总和。这种并行性通过有效利用多个 CPU 核心来提高性能，减少了整体计算时间。

## C# 12 和 .NET 8 中的额外优势和功能：

- 1. **资源消耗降低：** 与传统的同步编程相比，异步编程通过允许任务更高效地共享线程来减少资源消耗。这导致更好的资源利用率以及管理并发操作时更低的开销。
- 2. **无死锁的并发：** 异步编程通过允许任务非阻塞执行来帮助避免死锁。死锁可能在同步代码中发生，当多个线程竞争资源时，由于其协作式多任务的特性，异步代码中不太可能发生死锁。
- 3. **增强的错误处理：** C# 12 和 .NET 8 中的异步编程提供了改进的错误处理能力，使得处理异常和异步传播错误变得更容易。这有助于异步代码库的健壮性和可靠性。
- 4. **与现代 API 的集成：** 许多现代 API 和库设计为支持异步编程，使开发人员能够无缝利用异步模式。这包括 I/O 操作、网络通信和并发实用程序的异步版本。

异步编程为现代软件应用程序提供了显著的优势，例如改进的响应能力、可扩展性和性能。通过采用异步模式并利用 C# 12 和 .NET 8 提供的功能，开发人员可以创建高性能、可扩展且响应迅速的应用程序，以满足当今动态计算环境的需求。

## 异步编程的关键概念：任务、异步方法、await 关键字

异步编程是现代软件开发中的一个基本概念，尤其是在 C# 和 .NET 环境中。它允许开发人员编写可以执行非阻塞操作的代码，从而提高响应能力和可扩展性。在本讨论中，我们将探讨异步编程的关键概念，包括任务、异步方法和 `await` 关键字，并基于 C# 12 和 .NET 8 提供代码示例。

- 1. **任务：** C# 中的 `Task` 表示可与其他任务并发执行的异步操作。它是异步编程的基础构建块，用于表示可能需要时间完成的诸如 I/O 操作、计算或网络请求等操作。

### 创建和启动任务：

```csharp
public void StartTask()
{
    Task task = Task.Run(() =>
    {
        // Code to be executed asynchronously
        Console.WriteLine("Task is running asynchronously.");
    });

    // Continue other work while the task is running
    Console.WriteLine("Continuing with other work...");

    // Wait for the task to complete (optional)
    task.Wait(); // This blocks the main thread, use with caution
}
```

在此示例中，使用 `Task.Run` 创建并启动一个异步任务以打印消息。`Wait` 方法用于阻塞主线程并等待任务完成，但这是可选的，应谨慎使用以避免阻塞。

### 2. 异步方法：

C# 中的异步方法允许开发人员使用 `async` 和 `await` 关键字定义可异步执行的方法。异步方法返回 `Task` 或 `Task<T>`，表示异步操作的结果。

#### 定义和调用异步方法：

```csharp
public async Task<int> GetDataAsync()
{
    // Simulate an asynchronous operation (e.g., fetching data)
    await Task.Delay(2000); // Simulate 2 seconds delay
    return 42; // Simulated data
}
public async Task UseAsyncMethod()
{
    // Calling an asynchronous method using await
    int result = await GetDataAsync();
    Console.WriteLine($"Data received: {result}");
}
```

在此示例中，`GetDataAsync` 是一个异步方法，模拟了延迟 2 秒的数据获取操作。`await` 关键字用于异步等待方法完成并检索结果。

### 3. `await` 关键字：

`await` 关键字是 C# 异步编程的关键组成部分。它用于异步等待异步任务或方法完成。当遇到 `await` 表达式时，该方法会被暂停，而不会阻塞线程，直到被等待的任务完成。

#### 使用 `await` 关键字：

```csharp
public async Task ProcessDataAsync()
{
    // Asynchronously fetch data
    var dataTask = GetDataAsync();
    // Continue with other work while waiting for data
    Console.WriteLine("Processing other tasks while waiting for data...");
    // Wait for dataTask to complete and get the result
    int data = await dataTask;
    // Process the data
    Console.WriteLine($"Data processed: {data}");
}
```

在此示例中，`ProcessDataAsync` 方法异步调用 `GetDataAsync` 并使用 `await` 在数据检索操作完成前暂停执行。在等待期间，该方法可以并发执行其他任务。

### 重要注意事项：

- **异步方法返回 `Task` 或 `Task<T>`：** 异步方法如果不返回值应返回 `Task`，如果异步返回值则应返回 `Task<T>`。
- **避免 Async Void 方法：** 虽然可以定义返回类型为 `void` 的异步方法，但通常建议除事件处理程序外避免使用 `async void` 方法。改用 `async Task` 或 `async Task<T>`。
- **错误处理：** 异步方法可以像同步方法一样抛出异常。使用异步方法内的 `try-catch` 块处理异常，或使用 `Task` 或 `Task<T>` 将其传播到调用代码。

### 并发与性能：

异步编程通过允许多个任务在不阻塞主线程的情况下并发运行来实现并发。这种并发提高了性能，尤其是在涉及 I/O 密集型操作的场景中，等待外部资源可能耗时。

### 组合异步操作：

```csharp
public async Task<int> CombineAsyncOperations()
{
    Task<int> task1 = GetDataAsync(); // Asynchronous operation 1
    Task<int> task2 = GetDataAsync(); // Asynchronous operation 2

    // Await both tasks to complete
    int result1 = await task1;
    int result2 = await task2;

    return result1 + result2; // Combine results
}
```

在此示例中，两个异步操作并发启动，并在两个任务完成后使用 `await` 关键字组合其结果。

理解任务、异步方法和 `await` 关键字对于在 C# 和 .NET 中进行有效的异步编程至关重要。通过利用这些关键概念，开发人员可以创建响应迅速、可扩展且高性能的应用程序，能够在不阻塞主线程的情况下高效处理异步操作。C# 12 和 .NET 8 中的异步编程提供了强大的工具和模式，有效应对现代软件挑战。



## 探索异步编程在多个领域（如 Web 开发、UI 交互、云服务）中的实际应用

异步编程在软件开发的各个领域中都扮演着关键角色，能够带来响应性、可扩展性和性能上的提升。下面，我们以 C# 12 和 .NET 8 为例，通过示例和代码片段来探索异步编程在 Web 开发、UI 交互和云服务等领域中的实际应用。

### 1. Web 开发：

在 Web 开发中，异步编程对于高效处理并发请求、执行 I/O 密集型操作以及与外部 API 集成至关重要。以下是在 Web API 控制器中使用异步编程的示例：

```csharp
[ApiController]

[Route("api/[controller]")]

public class UsersController : ControllerBase
{

    private readonly IUserService _userService;

    public UsersController(IUserService userService)
    {
```

在数据检索、文件操作或网络请求等长时间运行的任务期间，我们来看一个 WPF 桌面应用程序中的示例：

```csharp
private async void LoadDataButton_Click(object sender,
RoutedEventArgs e)
{
    // Show loading indicator or disable UI controls

    // Asynchronously fetch data from a database or API
    var data = await DataService.GetDataAsync();

    // Update UI with the fetched data
    UpdateUIWithData(data);

    // Hide loading indicator or enable UI controls
}
```

在这个 WPF 应用程序中，LoadDataButton_Click 事件处理程序异步调用 DataService 类的 GetDataAsync 方法来获取数据。使用 async/await 可以确保在等待数据检索期间 UI 保持响应。

### 3. 云服务：

异步编程在云服务中非常普遍，用于处理文件上传、数据库查询和后台处理任务等异步操作。我们来看一个使用 Azure Blob Storage 将文件异步上传到云存储的示例：

```csharp
public async Task UploadFileToBlobAsync(string filePath)
{
    var blobClient = new BlobClient(connectionString, containerName, blobName);

    // Asynchronously upload the file to Azure Blob Storage

    await blobClient.UploadAsync(filePath, overwrite: true);
}
```

在此示例中，UploadFileToBlobAsync 方法使用 Azure.Storage.Blobs 包将文件异步上传到 Azure Blob Storage。异步编程确保文件上传操作不会阻塞主线程，从而使应用程序保持响应。

### 4. 异步 API 调用：

在与外部 API 交互时，异步编程至关重要，尤其是在处理网络延迟或长时间运行的操作时。我们来看一个使用 HttpClient 类发起异步 HTTP 请求的示例：

```csharp
public async Task<string> GetApiResponseAsync(string apiUrl)
{
    using var httpClient = new HttpClient();
    // Asynchronously send GET request and read response content
    var response = await httpClient.GetAsync(apiUrl);
    // Check if the response is successful
    response.EnsureSuccessStatusCode();
    // Read and return the response content as a string
    return await response.Content.ReadAsStringAsync();
}
```

在此示例中，GetApiResponseAsync 方法使用 HttpClient 向由 apiUrl 参数指定的 API 端点异步发送 GET 请求。该操作的异步特性确保了应用程序在等待 API 响应期间保持响应。

### 5. 并行处理：

异步编程对于并行处理任务也很有益处，在并行处理中，多个操作可以并发运行以提升性能。我们来看一个使用 async/await 和 Task.WhenAll 进行并行数据处理的示例：

# 第 2 章：利用顶级语句编写更简洁、更精炼的异步代码

在 C# 9 及更高版本中，使用顶级语句可以让开发者编写更简洁、更精炼的代码，尤其是在异步场景下。顶级语句消除了样板代码，使异步编程更直接、更易读。下面我们结合代码示例，探讨如何使用 C# 12 和 .NET 8 在异步代码中有效运用顶级语句。

### 1. 顶级语句概述：

顶级语句是在 C# 9 中引入的，用于简化入口点并减少代码文件中的仪式性代码。它们允许开发者在不显式编写命名空间、类声明或 Main 方法签名的情况下编写代码，使代码文件更专注于实际逻辑而非设置。

### 2. 在异步代码中使用顶级语句：

让我们通过一个示例来深入了解：我们将使用顶级语句创建一个异步程序，从 API 获取数据并异步处理。

### 示例：异步获取并处理数据

```csharp
using System;

using System.Net.Http;

using System.Threading.Tasks;

var apiUrl = "https://api.example.com/data";

async Task<string> FetchDataAsync(string url)
{
    using var httpClient = new HttpClient();
    var response = await httpClient.GetAsync(url);
    response.EnsureSuccessStatusCode();
    return await response.Content.ReadAsStringAsync();
}

async Task ProcessDataAsync(string data)
{
    // Simulate data processing asynchronously
    await Task.Delay(1000); // Simulate 1 second delay
    Console.WriteLine($"Processed data: {data}");
}

async Task Main()
{
    var data = await FetchDataAsync(apiUrl);
    await ProcessDataAsync(data);
}
```

在此示例中：

- 我们有一个顶级异步 Main 方法，它是程序的入口点。
- 我们定义了两个异步方法：
  - `FetchDataAsync` 用于从 API 获取数据，以及
  - `ProcessDataAsync` 用于处理获取到的数据。
- `Main` 方法使用 `FetchDataAsync` 异步获取数据，然后使用 `ProcessDataAsync` 处理数据。

### 3. 使用顶级语句编写异步代码的好处：

- **简洁性：** 顶级语句消除了显式类声明和 Main 方法声明的需要，使代码更简洁、更精炼。
- **聚焦逻辑：** 开发者可以更多地关注程序的实际逻辑，而不是样板设置代码。
- **可读性更强：** 代码中仪式性内容的减少使开发者更容易理解和维护异步代码库。

### 4. 在顶级异步代码中处理异常：

在处理异步代码时，异常处理至关重要。让我们增强之前的示例，加入错误处理：

```csharp
async Task<string> FetchDataAsync(string url)
{
    try
    {
        using var httpClient = new HttpClient();
        var response = await httpClient.GetAsync(url);
        response.EnsureSuccessStatusCode();
        return await response.Content.ReadAsStringAsync();
    }
    catch (HttpRequestException ex)
    {
        Console.WriteLine($"Error fetching data:\n{ex.Message}");
        throw; // Re-throw the exception
    }
}

async Task ProcessDataAsync(string data)
{
    try
    {
        // Simulate data processing asynchronously
        await Task.Delay(1000); // Simulate 1 second delay
        Console.WriteLine($"Processed data: {data}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error processing data: {ex.Message}");
    }
}
```

在此更新后的示例中，我们在 `FetchDataAsync` 和 `ProcessDataAsync` 方法中都添加了 try-catch 块，以优雅地处理潜在异常。`throw` 语句会重新抛出捕获的异常，使其在调用堆栈中向上传播。

### 5. 与异步流集成：

异步流是 C# 8 中引入的一项强大功能，可用于对数据集合进行异步迭代。让我们修改示例，使用异步流来获取和处理数据：

```csharp
async IAsyncEnumerable<string> FetchDataAsync(string url)
{
    using var httpClient = new HttpClient();
```





```csharp
var response = await httpClient.GetAsync(url);
response.EnsureSuccessStatusCode();
// Read data asynchronously in chunks
var stream = await response.Content.ReadAsStreamAsync();
using var reader = new System.IO.StreamReader(stream);
while (!reader.EndOfStream)
{
    yield return await reader.ReadLineAsync();
}
}
async Task ProcessDataAsync()
{
    await foreach (var line in FetchDataAsync(apiUrl))
    {
        // Process each line asynchronously
        await Task.Delay(500); // Simulate processing delay
        Console.WriteLine($"Processed line: {line}");
    }
}
```

在这个更新后的示例中，`FetchDataAsync` 返回一个异步字符串流，`ProcessDataAsync` 则异步处理从 API 获取的每一行数据。

在 C# 12 和 .NET 8 的异步编程中利用顶级语句带来了诸多好处，包括简洁性、可读性的提升，并且更关注逻辑本身而不是繁琐的仪式。通过利用顶级异步 `Main` 方法和简洁的 `async/await` 模式，开发者可以创建干净、高效的异步代码库，有效处理 API 交互、数据处理和错误处理等任务。顶级语句是 C# 语言的一项宝贵补充，尤其是在现代异步编程范式中。

## 利用异步流高效处理数据流（例如，网络通信、大型文件 I/O）

异步流在 C# 8 中引入，并在 C# 9 及更高版本中进一步增强，提供了一种异步高效处理数据流的强大机制。它们特别适用于网络通信、大型文件 I/O 以及其他流式数据源的场景。在本次讨论中，我们将探讨异步流的概念、其优点，并提供基于 C# 12 和 .NET 8 的代码示例，以展示它们在不同场景中的用法。

### 1. 理解异步流：

C# 中的异步流表示异步生成且可以异步消费的数据元素序列。它使开发者能够在不阻塞执行线程的情况下处理大型或无限数据流，从而提高响应性和资源利用率。

### 2. 异步流的优点：

- **高效内存使用：** 异步流允许惰性求值，即仅在需要时生成元素，从而降低大数据集的内存开销。
- **非阻塞处理：** 异步流支持非阻塞处理，在等待生成数据元素的同时，其他操作可以继续执行。
- **支持无限数据：** 异步流非常适合处理无限数据流或大小未知的数据源，例如实时数据馈送或连续传感器数据。

### 3. 使用异步流进行网络通信：

让我们从一个使用异步流进行网络通信的示例开始，在该示例中，我们从网络流异步读取数据：

```csharp
using System.IO;
using System.Net.Sockets;
using System.Threading.Tasks;

async Task ReadNetworkStreamAsync(TcpClient client)
```

在此示例中，`ReadDataAsync` 方法返回一个字节数组（`IAsyncEnumerable<byte[]>`）的异步流，这些字节数组表示从网络流中读取的数据块。`await foreach` 循环异步地从该流中消费数据块并进行处理。

### 4. 用于大型文件 I/O 的异步流：

异步流也有利于高效处理大型文件，而无需将整个文件加载到内存中。让我们考虑一个使用异步流异步读取大型文本文件的示例：

```csharp
async Task ReadLargeFileAsync(string filePath)
{
    await foreach (var line in ReadLinesAsync(filePath))
    {
        // Process each line asynchronously
        ProcessLine(line);
    }
}
async IAsyncEnumerable<string> ReadLinesAsync(string filePath)
{
    using StreamReader reader = new StreamReader(filePath);
```

```csharp
await foreach (var line in ReadLinesAsync(filePath))
{
    tasks.Add(ProcessLineAsync(line));
}

// Await all processing tasks to complete
await Task.WhenAll(tasks);
}
async Task ProcessLineAsync(string line)
{
    // Simulate asynchronous processing of a line
    await Task.Delay(100); // Simulate 100ms processing delay
    Console.WriteLine($"Processed line: {line}");
}
```

在这个修改后的示例中，`ProcessLargeFileAsync` 方法使用 `Task.WhenAll` 并行异步处理文件中的每一行。`ProcessLineAsync` 方法模拟每一行的异步处理，所有处理任务并发等待，以提高吞吐量。

C# 中的异步流为处理异步数据流（如网络通信、大型文件 I/O 和连续数据源）提供了一种强大而高效的机制。通过利用异步流，开发者在处理流式数据时可以编写出响应迅速、可扩展且内存高效的代码。C# 12 和 .NET 8 的异步编程为异步流提供了强大的支持，使开发者能够构建高性能应用程序，在各种场景中高效处理流式数据。

## 探索 C# 12 中其他与异步编程相关的功能（例如，静态异步方法、改进的模式匹配）

除了异步流和顶级语句之外，C# 12 还引入了其他几个与异步编程高度相关的功能。这些功能增强了异步代码的可读性、表现力和性能。让我们通过基于 C# 12 和 .NET 8 的代码示例，探索其中一些功能，包括静态异步方法、改进的模式匹配等。

### 1. 静态异步方法：

C# 12 允许将异步方法声明为静态，使开发者无需创建包含类的实例即可定义异步工具方法。这对于创建不依赖实例状态的异步辅助方法尤其有用。

**示例：用于文件 I/O 的静态异步方法**

```csharp
using System.IO;
using System.Threading.Tasks;

public static class FileHelper
{
    public static async Task<string> ReadFileAsync(string filePath)
    {
        using StreamReader reader = new StreamReader(filePath);
        return await reader.ReadToEndAsync();
    }
}
public class Program
{
    public static async Task Main()
    {
        string content = await FileHelper.ReadFileAsync("example.txt");
        Console.WriteLine(content);
    }
}
```

```csharp
Console.WriteLine("Collection of numbers: " +
    string.Join(", ", numbers));
    break;
    default:
        Console.WriteLine("Unknown data type");
        break;
    }
}
private async Task<bool> IsLongStringAsync(string str)
{
    await Task.Delay(100); // Simulate asynchronous operation
    return str.Length > 100;
}
}
public class Program
{
    public static async Task Main()
    {
        var processor = new DataProcessor();
        await processor.ProcessDataAsync("Lorem ipsum dolor sit amet");
        await processor.ProcessDataAsync(200);
        await processor.ProcessDataAsync(new List<int> { 1, 2, 3 });
    }
}
```

在此示例中，`DataProcessor` 类中的 `ProcessDataAsync` 方法使用模式匹配异步处理不同类型的数据。它使用 `IsLongStringAsync` 方法异步检查字符串是否较长，并使用模式匹配处理整数和整数集合。

### 3. 异步事件处理程序：

C# 12 允许将事件处理程序声明为异步，从而支持异步事件处理。这在 UI 编程和其他常见的异步操作事件驱动场景中特别有用。

**示例**：异步事件处理

```csharp
public class Button
{
    public event Func<Task> ClickedAsync;
    public async Task OnClickAsync()
    {
```





```
if (ClickedAsync != null)
    {
        await ClickedAsync();
    }
}
}
public class Program
{
    public static async Task Main()
    {
        var button = new Button();
        button.ClickedAsync += async () =>
        {
            await Task.Delay(1000); // Simulate asynchronous operation
            Console.WriteLine("Button clicked asynchronously");
        };
        await button.OnClickAsync();
    }
}
```

在此示例中，`Button` 类将 `ClickedAsync` 事件处理程序声明为异步。`Main` 方法异步订阅该事件，并通过模拟异步操作来异步处理点击事件。

## 4. 目标类型 `new` 表达式：

C# 12 引入了目标类型 `new` 表达式，允许开发者在实例化对象时省略类型名称，前提是类型可以从上下文中推断出来。此特性提升了代码的可读性和简洁性，特别是在异步编程场景中。

### 示例：使用异步方法的目标类型 `new` 表达式

```csharp
public class DataProcessor
{
    public async Task ProcessDataAsync()
    {
        var result = await GetDataAsync();
        Console.WriteLine("Processed data: " + result);
    }

    private async Task<string> GetDataAsync()
    {
        await Task.Delay(1000); // Simulate asynchronous operation
        return "Data";
    }
}
public class Program
{
    public static async Task Main()
    {
        var processor = new DataProcessor();
        await processor.ProcessDataAsync();
    }
}
```

在此示例中，`DataProcessor` 类使用目标类型 `new` 表达式实例化了一个 `Task.Delay` 对象，而无需显式指定类型名称。

C# 12 引入了多项增强异步编程的功能，包括静态异步方法、改进的模式匹配、异步事件处理程序以及目标类型 `new` 表达式。这些特性提升了代码的可读性、表现力和性能，使异步编程对开发者来说更加高效和愉悦。通过利用这些特性，开发者可以在 C# 中编写干净、简洁且高效的异步代码。

# 第 3 章

### 深入探索任务并行库（TPL）及其组件（任务、延续、取消）

C# 中的任务并行库（TPL）是一个用于并行和异步编程的强大框架。它为开发者提供了任务、延续和取消令牌等抽象，以高效管理并发和异步操作。在本探索中，我们将深入探讨 TPL 的组件，包括任务、延续、取消，并通过基于 C# 12 和 .NET 8 的代码示例演示它们的用法。

## 1. 任务并行库中的任务：

TPL 中的 `Task` 表示一项可以与其他任务并发运行的异步操作。它封装了操作的状态和结果，使得处理异步代码变得容易。

### 创建和运行任务：

```csharp
using System;
using System.Threading.Tasks;
public class Program
{
    public static async Task Main()
    {
        // Create and start a new task
        Task<int> task = Task.Run(() =>
        {
            return CalculateSum(10, 20);
        });
        // Wait for the task to complete and get the result
        int result = await task;
        Console.WriteLine("Sum: " + result);
    }
    public static int CalculateSum(int a, int b)
    {
        return a + b;
    }
}
```

在此示例中，我们使用 `Task.Run` 创建并运行一个任务，该任务异步执行 `CalculateSum` 方法并返回两个数字的和。

## 2. 任务延续：

任务延续允许你指定在任务完成后应执行的代码，无论任务是成功完成还是出现异常。这支持异步操作的链式调用和结果处理。

### 使用任务延续：

```csharp
public class Program
{
    public static async Task Main()
    {
        Task<int> initialTask = Task.Run(() =>
        {
            return CalculateSum(10, 20);
        });

        // Specify a continuation to execute when the initial task completes
        Task continuationTask = initialTask.ContinueWith(task =>
        {
            int result = task.Result;
            Console.WriteLine("Continuation Result: " + result);
        });

        await continuationTask; // Wait for the continuation to complete
    }
}

public static int CalculateSum(int a, int b)
{
    return a + b;
}
```

在此示例中，使用 `ContinueWith` 创建了一个延续任务，该任务在初始任务完成后执行，并打印计算结果。

## 3. 使用 CancellationToken 进行取消：

`CancellationToken` 提供了一种异步取消任务的机制。它允许优雅地取消操作并清理资源。

### 取消示例：

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;
public class Program
{
    public static async Task Main()
    {
        // Create a cancellation token source
        CancellationTokenSource cts = new CancellationTokenSource();
        CancellationToken token = cts.Token;

        // Start a task that can be cancelled
        Task longRunningTask = Task.Run(() =>
        {
            while (!token.IsCancellationRequested)
            {
                Console.WriteLine("Task running...");
                Thread.Sleep(1000); // Simulate work
            }
            Console.WriteLine("Task cancelled.");
        }, token);

        // Wait for user input to cancel the task
        Console.WriteLine("Press Enter to cancel the task.");
        Console.ReadLine();

        // Cancel the task using the cancellation token
        cts.Cancel();
        await longRunningTask; // Wait for the task to complete (optional)
    }
}
```

在此示例中，我们创建了一个取消令牌源（`CancellationTokenSource`），并在用户按下 Enter 时使用它来取消一个长时间运行的任务。

## 4. 任务异常处理：

TPL 中的任务支持异常处理，以处理异步操作期间发生的错误。你可以使用 `try/catch` 块或将 `await` 与 `Task.WhenAll` 结合使用来处理多个任务和异常。

### 异常处理示例：

```csharp
public class Program
{
    public static async Task Main()
    {
        Task<int> task1 = Task.Run(() =>
        {
            throw new Exception("Error in Task 1");
            return 0; // This line won't be reached
        });
        Task<int> task2 = Task.Run(() =>
        {
            throw new Exception("Error in Task 2");
            return 0; // This line won't be reached
        });
        try
        {
            await Task.WhenAll(task1, task2); // Wait for both tasks to complete
        }
        catch (Exception ex)
        {
            Console.WriteLine("Exception caught: " + ex.Message);
        }
    }
}
```

在此示例中，使用 `Task.WhenAll` 等待两个任务完成，任务抛出的任何异常都会在 `catch` 块中被捕获和处理。

## 5. 任务并行性与性能：

TPL 允许开发者通过并行运行任务来利用多核处理器的能力。这可以在 CPU 密集型和可并行化的工作负载中提高性能。

### 并行性示例：

```csharp
public class Program
{
    public static void Main()
    {
        Parallel.For(0, 10, i =>
        {
            Console.WriteLine($"Task {i} running on thread {Thread.CurrentThread.ManagedThreadId}");
            Thread.Sleep(1000); // Simulate work
        });
    }
}
```

在此示例中，使用 `Parallel.For` 并行运行多个任务，利用多个线程进行并发执行。

## 1.1 计算机发展简史

电子计算机是现代科学技术的一项卓越成就。1946年，世界上第一台通用电子数字计算机ENIAC在美国宾夕法尼亚大学研制成功，标志着人类进入电子计算机时代。

- 1. 第一代计算机（电子管时代）：1946—1958年
- 2. 第二代计算机（晶体管时代）：1958—1964年
- 3. 第三代计算机（集成电路时代）：1964—1971年
- 4. 第四代计算机（大规模集成电路时代）：1971年至今

```csharp
using System;
using System.Threading.Tasks;
public class Program
{
    public static async Task Main()
    {
        // Example of CPU-bound work offloaded to a background thread
        Task<int> task = Task.Run(() =>
        {
            return CalculateSum(10, 20);
        });
        // Continue asynchronously after the task completes
        int result = await task;
        Console.WriteLine("Sum: " + result);
    }
    public static int CalculateSum(int a, int b)
    {
        // Simulate CPU-bound work
        int sum = 0;
        for (int i = a; i <= b; i++)
```




```csharp
{
    sum += i;
}
    return sum;
}
}
```

在此示例中，使用 `Task.Run` 在后台线程上异步运行 `CalculateSum` 方法，并在 `Main` 方法中异步等待结果。

## 2. TaskCompletionSource 用于自定义异步操作：

`TaskCompletionSource` 是创建自定义异步操作的强大机制，这些操作无法直接映射到传统的 async 方法。它允许开发人员手动控制任务的完成。

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
```

(`PerformCustomOperationAsync`) 中，我们模拟异步延迟然后使用 `SetResult` 设置结果。

## 3. 任务延续用于顺序操作：

任务延续允许按顺序链接异步操作，确保一个任务在另一个任务完成后才开始。这对于定义异步操作的工作流程非常有用。

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Task<int> initialTask = Task.Run(() =>
        {
            return CalculateSum(10, 20);
        });
        Task<string> continuationTask = initialTask.ContinueWith(task =>
        {
            int result = task.Result;
            return $"Sum: {result}";
        });
        string result = await continuationTask;
        Console.WriteLine(result);
    }
    public static int CalculateSum(int a, int b)
    {
        return a + b;
    }
}
```

在此示例中，使用 `ContinueWith` 定义一个延续任务，该任务处理初始任务 (`CalculateSum`) 的结果并返回格式化的字符串。

## 4. 使用任务进行异常处理：

在异步操作中处理异常对于健壮的错误处理至关重要。TPL 中的任务提供了在异步执行期间捕获和处理异常的机制。

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            Task<int> task = Task.Run(() =>
            {
                throw new InvalidOperationException("Invalid operation");
                return 0; // This line won't be reached
            });
            int result = await task; // This line throws an exception
        }
        catch (Exception ex)
        {
            Console.WriteLine("Exception caught: " + ex.Message);
        }
    }
}
```

在此示例中，`Task.Run` 操作抛出 `InvalidOperationException`，该异常在 `Main` 方法的 `catch` 块中被捕获并处理。

## 5. 使用 async/await 编写异步代码：

C# 中的 `async/await` 关键字提供了一种更自然、更易读的方式来编写异步代码。`async` 方法可以在不阻塞执行线程的情况下等待异步操作。

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        int result = await CalculateSumAsync(10, 20);
        Console.WriteLine("Sum: " + result);
    }
    public static async Task<int> CalculateSumAsync(int a, int b)
    {
        await Task.Delay(1000); // Simulate asynchronous delay
```

```csharp
Task<int> task1 = Task.Run(() => DelayedOperation(1, 2000));

Task<int> task2 = Task.Run(() => DelayedOperation(2, 1500));

// Wait for the first task to complete
Task<int> firstCompletedTask = await Task.WhenAny(task1, task2);

Console.WriteLine("First task completed:");

Console.WriteLine("First Completed Task Result: " + firstCompletedTask.Result);
}

public static int DelayedOperation(int id, int delay)
{
    Task.Delay(delay).Wait(); // Simulate delay
    return id;
}
}
```

在此示例中，使用 `Task.WhenAny` 等待 `task1` 和 `task2` 中最先完成的任务。最快的任务完成时间反映在输出中。

## 3. `Task.WaitAll` 用于同步等待：

```csharp
Task<int> task3 = Task.Run(() => DelayedOperation(3, 1000));

// Await the completion of the first group of tasks among task1, task2, and task3

Task<int>[] firstGroupTasks = { task1, task2, task3 };

Task<int>[] completedTasks = await Task.WhenAny(Task.WhenAll(firstGroupTasks), Task.WhenAny(firstGroupTasks));

Console.WriteLine("First group of tasks completed:");

foreach (var completedTask in completedTasks)
{
    Console.WriteLine("Completed Task Result: " + completedTask.Result);
}
}

public static int DelayedOperation(int id, int delay)
{
    Task.Delay(delay).Wait(); // Simulate delay
    return id;
}
}
```

```csharp
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        string filePath = "example.txt";
        try
        {
            string content = await ReadFileAsync(filePath);
            Console.WriteLine("File content:");
            Console.WriteLine(content);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error reading file: " + ex.Message);
        }
    }

    public static async Task<string> ReadFileAsync(string filePath)
    {
        using StreamReader reader = new StreamReader(filePath);

        return await reader.ReadToEndAsync();
    }
}
```

在此示例中，`ReadFileAsync` 使用 `StreamReader.ReadToEndAsync` 异步读取文件内容。`Main` 方法等待此异步操作的结果，而不会阻塞主线程。

## 异步写入文件：

```csharp
using System;
using System.IO;
using System.Text;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        string filePath = "output.txt";

        string content = "Hello, async/await!";
```

```csharp
Console.WriteLine(response);
}
catch (Exception ex)
{
    Console.WriteLine("Error fetching data: " + ex.Message);
}
}

public static async Task<string> GetApiResponseAsync(string url)
{
    HttpResponseMessage response = await client.GetAsync(url);

    response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)

    return await response.Content.ReadAsStringAsync();
}
}
```

在此示例中，`GetApiResponseAsync` 使用 `HttpClient.GetAsync` 异步发出 HTTP GET 请求，并使用 `ReadAsStringAsync` 异步读取响应内容。

```csharp
Console.WriteLine($"Product ID: {product.Id}, Name: {product.Name}");
}
}
catch (Exception ex)
{
    Console.WriteLine("Error executing query: " + ex.Message);
}
}

public static async Task<List<Product>> GetProductsAsync(string query)
{
    using SqlConnection connection = new SqlConnection(connectionString);
    using SqlCommand command = new SqlCommand(query, connection);
    await connection.OpenAsync();
    SqlDataReader reader = await command.ExecuteReaderAsync();
    var products = new List<Product>();
    while (await reader.ReadAsync())
    {
        products.Add(new Product
        {
            Id = Convert.ToInt32(reader["Id"]),
            Name = reader["Name"].ToString()
        });
    }
    return products;
}
}

public class Product
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

在此示例中，`GetProductsAsync` 使用 `SqlCommand.ExecuteReaderAsync` 异步执行 SQL 查询，并使用 `ReadAsync` 异步读取结果。

使用 `async/await` 实现异步 I/O 操作对于构建响应迅速且可扩展的应用程序至关重要。无论是处理文件 I/O、网络操作还是数据库交互，利用异步编程可确保应用程序

通过避免阻塞主线程保持响应性。通过使用 async/await 与 `System.IO`、`System.Net.Http` 或数据库库等提供的适当异步 API，开发人员可以设计能够高效处理 I/O 绑定任务并提供流畅用户体验的应用程序。理解和掌握异步编程技术是构建高性能应用程序的现代 C# 和 .NET 开发的关键。

## 使用 async/await 处理具有多个结果和异常的异步操作

在异步编程中，处理多个结果和异常对于构建健壮可靠的应用程序至关重要。C# 中的 `async/await` 关键字提供了一种方便直观的方式来处理异步操作，允许开发人员并发等待多个任务，处理其结果或异常，并优雅地管理异步工作流。在本次探索中，我们将深入探讨使用 `async/await` 处理具有多个结果和异常的异步操作，并提供基于 C# 12 和 .NET 8 的代码示例。

### 1. 使用 `async/await` 并发处理多个任务：

处理多个异步操作时，可以使用 `async/await` 并发等待其完成。这允许任务并行执行，提高整体性能和响应能力。

**示例**：并发处理多个任务：

```
return id;
}
}
```

在此示例中，使用 `Task.Run` 并发启动两个任务。`await` 关键字用于等待两个任务完成，以便检索和处理其结果。

### 2. 使用 `async/await` 处理异常：

等待多个任务时，处理执行期间可能发生的任何异常至关重要。

`async/await` 通过允许您在 `await` 语句周围使用 `try/catch` 块来捕获被等待任务抛出的异常，从而简化了错误处理。

**示例**：使用多个任务处理异常：

```csharp
using System;

using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
```
```
}
    public static int ThrowExceptionAfterDelay(int id, int delay)
    {
        Task.Delay(delay).Wait(); // Simulate delay
        throw new Exception("Exception thrown by task " + id);
    }
}
```

在此示例中，`ThrowExceptionAfterDelay` 模拟了一个在延迟后抛出异常的任务。`await` 语句周围的 `try/catch` 块捕获被等待任务抛出的任何异常。

### 3. 使用 `Task.WhenAll` 处理多个结果和异常：

要等待多个任务并集体处理其结果或异常，可以使用 `Task.WhenAll`。此方法返回一个任务，该任务在所有提供的任务完成后完成，允许您并行等待多个任务的完成。

**示例**：使用 `Task.WhenAll` 处理多个结果和异常：

```csharp
using System;
```
```csharp
using System.Threading.Tasks;
public class Program
{
    public static async Task Main()
    {
        Task<int> task1 = Task.Run(() => DelayedOperation(1, 2000));
        Task<int> task2 = Task.Run(() => ThrowExceptionAfterDelay(2, 1500));
        // Await the completion of all tasks and handle results/exceptions
        try
        {
            await Task.WhenAll(task1, task2);
            Console.WriteLine("All tasks completed successfully:");
            Console.WriteLine("Task 1 Result: " + task1.Result);
            Console.WriteLine("Task 2 Result: " + task2.Result);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}
```

```
}
}
public static int DelayedOperation(int id, int delay)
{
    Task.Delay(delay).Wait(); // Simulate delay
    return id;
}
public static int ThrowExceptionAfterDelay(int id, int delay)
{
    Task.Delay(delay).Wait(); // Simulate delay
    throw new Exception("Exception thrown by task " + id);
}
}
```

在此示例中，使用 `Task.WhenAll` 并发等待两个任务的完成。`Task.WhenAll` 周围的 `try/catch` 块捕获被等待任务抛出的任何异常。

使用 `async/await` 处理具有多个结果和异常的异步操作对于构建可靠且健壮的应用程序至关重要。无论是并发等待多个任务的完成、处理被等待任务抛出的异常，还是使用 `Task.WhenAll` 集体等待多个任务的完成，`async/await` 都提供了一种方便直观的方式在 C# 和 .NET 中处理异步操作。通过掌握这些技术，开发人员可以构建能够优雅处理异步工作流的应用程序，确保在各种场景下的响应性和可靠性。

## 使用 await 关键字链接异步操作并探索最佳实践

链接异步操作是现代 C# 和 .NET 开发中的常见做法，尤其是在处理依赖于其他异步任务完成的任务时。`await` 关键字在链接异步操作中发挥着关键作用，使开发人员能够编写干净、顺序的代码，同时利用异步编程的强大功能。在本次探索中，我们将深入探讨使用 `await` 链接异步操作的最佳实践，并提供基于 C# 12 和 .NET 8 的代码示例。

### 1. 异步任务的顺序链接：

`await` 的主要优点之一是能够顺序链接异步任务，确保一个任务仅在前一个任务完成后才开始。这种顺序链接有助于保持代码清晰度和逻辑流程。

### 示例：任务的顺序链接

```csharp
using System;
```
```
using System.Threading.Tasks;
public class Program
{
    public static async Task Main()
    {
        // Sequential chaining of asynchronous tasks
        int result1 = await Task1();
        int result2 = await Task2(result1);
        int finalResult = await Task3(result2);
        Console.WriteLine("Final Result: " + finalResult);
    }
    public static async Task<int> Task1()
    {
        await Task.Delay(1000); // Simulate asynchronous delay
        return 10;
    }
    public static async Task<int> Task2(int input)
    {
        await Task.Delay(1500); // Simulate asynchronous delay
```

```
public class Program
{
    public static void Main()
    {
        Task<int> resultTask = Task.Run(() => CalculateSum(10, 20));

        int result = resultTask.Result; // Blocking call
        Console.WriteLine("Sum: " + result);
    }

    public static int CalculateSum(int a, int b)
    {
        return a + b;
    }
}
```

在此示例中，使用 `Task.Run` 在后台线程上运行同步方法（`CalculateSum`）。由于该方法是同步的且不执行任何异步操作，因此无需 `async/await` 使用 `Task.Run` 就足够了。

### 3. 链接任务中的异常处理：

链接异步任务时，适当的异常处理至关重要。每个被等待的任务都应包装

在 `try/catch` 块中以处理执行期间可能发生的任何异常。

### **示例：** 链接任务中的异常处理

```csharp
using System;

using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            int result1 = await Task1();
            int result2 = await Task2(result1);
            int finalResult = await Task3(result2);
            Console.WriteLine("Final Result: " + finalResult);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}
```
```
}
public static async Task<int> Task1()
{
    await Task.Delay(1000); // Simulate asynchronous delay
    return 10;
}
public static async Task<int> Task2(int input)
{
    await Task.Delay(1500); // Simulate asynchronous delay
    if (input < 0) throw new InvalidOperationException("Invalid input");
    return input * 2;
}
public static async Task<int> Task3(int input)
{
    await Task.Delay(2000); // Simulate asynchronous delay
    return input + 5;
}
}




在这个例子中，`Task2` 包含一个验证检查，如果输入为负数，它会抛出`InvalidOperationException`。`Main` 方法中的`try/catch` 块会处理链式任务抛出的任何异常。

### 4. 使用 Task.WhenAll 进行并行执行：

有时，顺序链式任务并非必要，尤其是当任务彼此独立且可以并发执行时。在这种情况下，可以使用`Task.WhenAll` 并行等待多个任务。

### 示例：使用 Task.WhenAll 进行并行执行

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Task<int> task1 = Task1();
        Task<int> task2 = Task2();
        Task<int> task3 = Task3();

        await Task.WhenAll(task1, task2, task3);

        Console.WriteLine("All tasks completed:");
        Console.WriteLine("Task 1 Result: " + task1.Result);
        Console.WriteLine("Task 2 Result: " + task2.Result);
        Console.WriteLine("Task 3 Result: " + task3.Result);
    }

    public static async Task<int> Task1()
    {
        await Task.Delay(1000); // Simulate asynchronous delay
        return 10;
    }

    public static async Task<int> Task2()
    {
        await Task.Delay(1500); // Simulate asynchronous delay
        return 20;
    }

    public static async Task<int> Task3()
    {
        await Task.Delay(2000); // Simulate asynchronous delay
```

```csharp
// Uncommenting the following line would cause a deadlock
// int result = task.Result;
int result = await task;
Console.WriteLine("Result: " + result);
}
public static async Task<int>
LongRunningOperationAsync()
{
    await Task.Delay(2000); // Simulate long-running asynchronous operation
    return 42;
}
```

在这个例子中，在`Main` 方法中直接访问`task.Result` 会导致死锁，因为它会阻塞主线程，等待异步任务同步完成。相反，使用`await` 可以异步等待任务完成，而不会阻塞。

使用`await`关键字链式执行异步操作是在C#和.NET中构建响应式且高效异步工作流的强大技术。通过遵循最佳实践，如顺序链式、正确的异常处理、避免不必要的`async/await`、使用`Task.WhenAll`进行并行执行以及防止死锁，开发者可以编写干净、可维护且高性能的异步代码。理解这些最佳实践并掌握异步编程技术对于现代软件开发至关重要，尤其是在响应性和可扩展性至关重要的场景中。

# 第 5 章：利用异步编程进行网络通信（例如，HTTP请求/响应）

异步编程在处理网络通信任务中扮演着至关重要的角色，尤其是在现代应用程序中处理HTTP请求/响应时。异步操作允许应用程序执行非阻塞I/O操作，确保响应性和可扩展性。在本探讨中，我们将深入了解如何利用异步编程进行网络通信，重点介绍使用C# 12和.NET 8异步发出HTTP请求和处理响应。

### 1. 发出异步HTTP GET请求：

在应用程序中，异步发出HTTP GET请求是与Web API通信或从远程服务器获取数据的常见场景。.NET中的`HttpClient`类提供了异步发出HTTP请求的方法。

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main()
    {
        string url = "https://jsonplaceholder.typicode.com/posts/1";
        try
        {
            string response = await GetApiResponseAsync(url);
            Console.WriteLine("Response from API:");
            Console.WriteLine(response);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error fetching data: " + ex.Message);
        }
    }

    public static async Task<string> GetApiResponseAsync(string url)
    {
        HttpResponseMessage response = await client.GetAsync(url);
        response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)

        return await response.Content.ReadAsStringAsync();
    }
}
```

### 2. 发出异步HTTP POST请求：

类似地，异步发出HTTP POST请求对于向远程服务器或API发送数据至关重要。`HttpClient`类也提供了发出异步POST请求的方法。

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main()
    {
        string url = "https://jsonplaceholder.typicode.com/posts";
        string postData = "{\"title\": \"New Post\", \"body\": \"This is a new post.\", \"userId\": 1}";

        try
        {
            string response = await PostDataAsync(url, postData);
            Console.WriteLine("Response from API:");
            Console.WriteLine(response);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error posting data: " + ex.Message);
        }
    }

    public static async Task<string> PostDataAsync(string url, string postData)
    {
        var content = new StringContent(postData, Encoding.UTF8, "application/json");
        HttpResponseMessage response = await client.PostAsync(url, content);
        response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)

        return await response.Content.ReadAsStringAsync();
    }
}
```

### 3. 异步响应处理和错误管理：

异步编程允许高效处理HTTP响应和错误管理。`HttpClient`方法返回`Task<HttpResponseMessage>`或`Task<HttpResponseMessage>`类型，使开发者能够等待响应并异步处理它。

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main()
    {
        string url = "https://jsonplaceholder.typicode.com/posts/1000"; // Invalid URL
        try
        {
            HttpResponseMessage response = await client.GetAsync(url);
            if (response.IsSuccessStatusCode)
            {
                string responseData = await response.Content.ReadAsStringAsync();
                Console.WriteLine("Response data:");
                Console.WriteLine(responseData);
            }
            else
            {
                Console.WriteLine("HTTP Error: " + response.StatusCode);
            }
        }
        catch (HttpRequestException ex)
        {
            Console.WriteLine("HTTP Request Error: " + ex.Message);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
}
```

### 4. 管理多个异步请求：

在需要并发发出多个异步请求的场景中，可以使用`Task.WhenAll`高效地等待所有任务完成。

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient client = new HttpClient();

    public static async Task Main()
    {
        Task<string> task1 = GetApiResponseAsync("https://jsonplaceholder.typicode.com/posts/1");
        Task<string> task2 = GetApiResponseAsync("https://jsonplaceholder.typicode.com/posts/2");
        Task<string> task3 = GetApiResponseAsync("https://jsonplaceholder.typicode.com/posts/3");

        await Task.WhenAll(task1, task2, task3);

        Console.WriteLine("All requests completed:");
        Console.WriteLine("Response 1: " + task1.Result);
        Console.WriteLine("Response 2: " + task2.Result);
        Console.WriteLine("Response 3: " + task3.Result);
    }
}
```



```
}
    public static async Task<string>
GetApiResponseAsync(string url)
{
    HttpResponseMessage response = await client.GetAsync(url);
    response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)
    return await response.Content.ReadAsStringAsync();
}
},
在此示例中，使用 `Task.WhenAll` 来等待使用 `GetApiResponseAsync` 方法并发执行的多个异步 HTTP GET 请求完成。

利用 C# 和 .NET 中的异步编程进行网络通信对于构建响应迅速且可扩展的应用程序至关重要。使用 `HttpClient` 进行异步 HTTP 请求/响应以及对响应和错误的异步处理可确保资源的高效利用和应用程序性能的提升。通过遵循最佳实践并利用 `async/await` 等特性，开发人员可以设计出能够顺畅处理网络通信任务的应用程序，为与远程 API 或服务交互的用户提供无缝体验。理解异步编程的细微差别是现代软件开发的基础，尤其是在分布式系统和云应用程序中。

## 使用链式异步方法构建复杂场景的异步工作流

使用链式异步方法构建异步工作流是现代软件开发中的一种强大技术，尤其适用于处理任务相互依赖或需要协调的复杂场景。异步工作流通过避免阻塞操作并高效利用系统资源，有助于实现响应性和可扩展性。在本次探索中，我们将深入介绍如何使用 C# 12 和 .NET 8 构建链式异步方法的异步工作流，并通过代码示例说明各种复杂场景。

### 1. 顺序工作流中的链式异步方法：

在顺序工作流中，一个异步方法依赖于另一个方法的结果。链式调用这些方法可以在保持操作异步特性的同时实现任务的逐步执行。

**示例**：顺序链式异步方法

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            int result = await Task1();
            Console.WriteLine("Result from Task1: " + result);

            result = await Task2(result);
            Console.WriteLine("Result from Task2: " + result);

            result = await Task3(result);
            Console.WriteLine("Final Result: " + result);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }

    public static async Task<int> Task1()
    {
        await Task.Delay(1000); // Simulate asynchronous delay
        return 10;
    }

    public static async Task<int> Task2(int input)
    {
        await Task.Delay(1500); // Simulate asynchronous delay
        return input * 2;
    }

    public static async Task<int> Task3(int input)
    {
        await Task.Delay(2000); // Simulate asynchronous delay
        return input + 5;
    }
}
```

在此示例中，`Task1`、`Task2` 和 `Task3` 使用 `await` 顺序链式调用。每个方法执行一个异步操作并将其结果传递给链中的下一个方法。

### 2. 并行执行并合并结果：

在某些场景中，多个异步任务可以并发执行，其结果可以合并或进一步处理。`Task.WhenAll` 是用于并行执行任务并等待其完成的有用构造。

### 示例：异步方法的并行执行

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            Task<int> task1 = Task1();
            Task<int> task2 = Task2();
            Task<int> task3 = Task3();

            await Task.WhenAll(task1, task2, task3);

            int sum = task1.Result + task2.Result + task3.Result;
            Console.WriteLine("Sum of results: " + sum);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }

    public static async Task<int> Task1()
    {
        await Task.Delay(1000); // Simulate asynchronous delay
        return 10;
    }
    public static async Task<int> Task2()
    {
        await Task.Delay(1500); // Simulate asynchronous delay
        return 20;
    }
    public static async Task<int> Task3()
    {
        await Task.Delay(2000); // Simulate asynchronous delay
        return 30;
    }
}
```

在此示例中，`Task1`、`Task2` 和 `Task3` 使用 `Task.WhenAll` 并发执行，其结果被合并以计算总和。

### 3. 处理具有依赖关系的多个任务：

有时，任务之间存在依赖关系，即一个任务的执行需要另一个任务的结果。在这种情况下，按正确顺序等待任务对于维护工作流至关重要。

### 示例：处理具有依赖关系的任务

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            Task<int> task1 = Task1();
            Task<int> task2 = Task2(await task1);
            await Task.WhenAll(task1, task2);
            Console.WriteLine("Result from Task2: " + task2.Result);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }
    public static async Task<int> Task1()
    {
        await Task.Delay(1000); // Simulate asynchronous delay
        return 10;
    }
    public static async Task<int> Task2(int input)
    {
        await Task.Delay(1500); // Simulate asynchronous delay
        return input * 2;
    }
}
```

在此示例中，`Task2` 依赖于 `Task1` 的结果，因此 `Task2` 在执行前等待 `Task1`。

### 4. 错误处理和重试逻辑：

异步工作流应包含健壮的错误处理，并在某些情况下包含重试逻辑以处理瞬时错误或网络问题。

### **示例**：错误处理和重试逻辑

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        try
        {
            await RetryOperationAsync();
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error: " + ex.Message);
        }
    }

    public static async Task RetryOperationAsync()
    {
        int retryCount = 3;
        int delayMs = 1000;

        while (retryCount > 0)
        {
            try
            {
                // Perform asynchronous operation
                await Task.Delay(delayMs); // Simulate operation
                Console.WriteLine("Operation completed successfully.");
                return; // Exit loop if successful
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error in operation: " + ex.Message);
                retryCount--;
                if (retryCount > 0)
                {
                    Console.WriteLine($"Retrying in {delayMs} ms...");
                    await Task.Delay(delayMs); // Retry after delay
                }
            }
        }
        throw new InvalidOperationException("Operation failed after retries.");
    }
}
```

在此示例中，`RetryOperationAsync` 演示了异步操作的重试逻辑。它会在延迟后多次重试操作，并在所有重试均失败时抛出异常。

使用链式异步方法构建异步工作流对于处理复杂场景并实现响应迅速且可扩展的应用程序至关重要。通过在异步工作流中结合顺序执行、并行、错误处理和重试逻辑，开发人员可以创建健壮且高效的系统，以优雅的方式处理各种场景。理解异步编程的细微差别并掌握 `async/await`、`Task.WhenAll` 以及适当的错误处理技术的用法，是设计利用 C# 和 .NET 中异步编程全部潜力的现代应用程序的基础。

## 为高效资源利用实现并发异步操作

在现代软件开发中，高效的资源利用对于构建高性能应用程序至关重要。C# 和 .NET 中的异步编程提供了强大的工具和模式来实现并发异步操作，使应用程序能够高效利用系统资源。在本次探索中，我们将深入介绍如何使用 C# 12 和 .NET 8 实现并发异步操作，并通过代码示例演示高效的资源利用。

### 1. 使用 Task.WhenAll 进行并行执行：

`Task.WhenAll` 是 C# 和 .NET 中用于异步任务并行执行的一个强大构造。它允许多个任务并发运行，然后等待其完成，这有利于利用 CPU 核心并减少总体执行时间。

### 示例：使用 Task.WhenAll 进行并行执行

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Task<int> task1 = Task1();
        Task<int> task2 = Task2();
        Task<int> task3 = Task3();



```csharp
await Task.WhenAll(task1, task2, task3);
Console.WriteLine("All tasks completed:");
Console.WriteLine("Task 1 Result: " + task1.Result);
Console.WriteLine("Task 2 Result: " + task2.Result);
Console.WriteLine("Task 3 Result: " + task3.Result);
}
public static async Task<int> Task1()
{
    await Task.Delay(1000); // Simulate asynchronous delay
    return 10;
}
public static async Task<int> Task2()
{
    await Task.Delay(1500); // Simulate asynchronous delay
    return 20;
}
public static async Task<int> Task3()
{
    await Task.Delay(2000); // Simulate asynchronous delay
    return 30;
}
}
```

在此示例中，使用了 `Task.WhenAll` 并发执行 `Task1`、`Task2` 和 `Task3`，然后等待其完成。这种方法通过允许任务并行运行来最大化 CPU 利用率。

## 2. 使用 SemaphoreSlim 限制并发任务：

虽然并发执行是有益的，但在某些情况下，限制并发任务的数量是必要的，以避免压垮系统资源。`SemaphoreSlim` 是一种同步原语，可用于限制对资源的并发访问。

### 示例：使用 SemaphoreSlim 限制并发任务

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

public class Program
{
    private static SemaphoreSlim semaphore = new SemaphoreSlim(2); // Limit to 2 concurrent tasks

    public static async Task Main()
    {
        Task task1 = Task.Run(() => PerformTask(1));
        Task task2 = Task.Run(() => PerformTask(2));
        Task task3 = Task.Run(() => PerformTask(3));
        Task task4 = Task.Run(() => PerformTask(4));

        await Task.WhenAll(task1, task2, task3, task4);
    }

    public static async Task PerformTask(int id)
    {
        await semaphore.WaitAsync(); // Wait until semaphore available
        try
        {
            Console.WriteLine($"Task {id} started");
            await Task.Delay(1000); // Simulate asynchronous delay
            Console.WriteLine($"Task {id} completed");
        }
        finally
        {
            semaphore.Release(); // Release semaphore
        }
    }
}
```

在此示例中，使用 `SemaphoreSlim` 限制对 `PerformTask` 方法的并发访问。由于信号量限制，同时只能运行两个任务，从而防止资源利用过度。

## 3. 使用 async/await 进行并发 I/O 操作：

异步编程对于 I/O 密集型操作非常有益，例如读写文件、访问数据库或进行网络调用。I/O 操作的并发执行可以显著提高应用程序的响应能力。

### 示例：并发文件 I/O 操作

```csharp
using System;
using System.IO;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Task<string> readTask = ReadFileAsync("data.txt");
        Task writeTask = WriteFileAsync("output.txt", "Hello, Async!");

        await Task.WhenAll(readTask, writeTask);
}
```

### 示例：结合并发与错误处理

```csharp
using System;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        Task<int> task1 = Task.Run(() =>
        PerformOperation(1));
        Task<int> task2 = Task.Run(() =>
        PerformOperation(2));

        try
        {
            await Task.WhenAll(task1, task2);
            Console.WriteLine("All operations completed:");
            Console.WriteLine("Result 1: " + task1.Result);
            Console.WriteLine("Result 2: " + task2.Result);
        }
        catch (AggregateException ex)
        {
            Console.WriteLine("Error in one or more operations:");
            foreach (var innerEx in ex.InnerExceptions)
            {
                Console.WriteLine(innerEx.Message);
            }
        }
    }

    public static int PerformOperation(int id)
    {
        if (id == 2)
        {
            throw new InvalidOperationException("Operation failed for id 2");
        }
        return id * 10;
    }
}
```

在此示例中，`Task.WhenAll` 与使用 `try/catch` 的错误处理相结合。如果任何操作抛出异常，它将被捕获在 `AggregateException` 中，从而允许进行适当的错误报告。

实现并发异步操作对于高效利用资源和提高应用程序性能至关重要。无论是使用 `Task.WhenAll` 进行并行执行、使用 `SemaphoreSlim` 限制并发，还是将 async/await 与 I/O 操作结合，理解并利用这些技术都可以显著增强应用程序的响应能力和可扩展性。在 C# 和 .NET 中设计并发异步工作流时，必须考虑任务的性质、资源限制和错误处理策略。掌握这些概念使开发人员能够构建健壮、高性能的应用程序，充分利用异步编程的全部潜力。

## 利用 .NET 库（如 HttpClient 和 Entity Framework Core 8（如果适用））中的异步功能

利用 .NET 库（如 HttpClient 和 Entity Framework Core 6（撰写本文时为最新版本））中的异步功能对于构建高性能和可扩展的应用程序至关重要。异步编程使这些库能够高效处理 I/O 密集型操作，例如发出 HTTP 请求或访问数据库，而不会阻塞主线程。在本次探索中，我们将深入了解如何使用 C# 12 和 .NET 8 利用这些库中的异步功能，并通过代码示例展示最佳实践。

### 1. 使用 HttpClient 进行异步 HTTP 请求：

.NET 中的 `HttpClient` 类广泛用于向 Web API 发出 HTTP 请求，并提供异步方法以实现高效的网络通信。`HttpClient` 中的异步方法允许应用程序执行非阻塞 HTTP 请求，从而提高响应能力。

### 示例：使用 HttpClient 进行异步 HTTP GET 请求

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient httpClient = new HttpClient();

    public static async Task Main()
    {
        string url = "https://jsonplaceholder.typicode.com/posts/1";

        try
        {
            HttpResponseMessage response = await httpClient.GetAsync(url);
            response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)

            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine("Response from API:");
            Console.WriteLine(responseBody);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error fetching data: " + ex.Message);
        }
    }
}
```

在此示例中，`httpClient.GetAsync` 是一个异步方法，它异步地向指定 URL 发出 HTTP GET 请求。`await` 关键字用于异步等待响应，而不会阻塞主线程。

### 2. 使用 Entity Framework Core 进行异步数据库操作：

Entity Framework Core (EF Core) 是 .NET 中用于数据库访问的流行对象关系映射（ORM）框架。EF Core 支持数据库操作的异步方法，允许应用程序异步执行数据库查询和更新。

### 示例：使用 Entity Framework Core 进行异步查询

假设我们有一个 `Post` 实体和 `DbContext` 设置：

```csharp
using System;
using Microsoft.EntityFrameworkCore;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        using (var context = new BlogDbContext())
        {
            try
            {
                var posts = await context.Posts.ToListAsync();
                foreach (var post in posts)
                {
                    Console.WriteLine($"PostId: {post.Id}, Title: {post.Title}");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine("Error fetching posts: " + ex.Message);
            }
        }
    }
}

public class Post
{
    public int Id { get; set; }
    public string Title { get; set; }
    // Other properties
}

public class BlogDbContext : DbContext
{
    public DbSet<Post> Posts { get; set; }
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
}
```



{
    optionsBuilder.UseSqlServer("your_connection_string")
;
  }
}
```

在这个示例中，`ToListAsync` 是 EF Core 提供的异步方法，用于异步获取数据库中的所有帖子。`await` 关键字用于等待查询异步完成。

## 3. Asynchronous Inserts and Updates with EF Core:

EF Core 还支持数据库插入、更新和删除的异步方法。异步数据库操作对于需要在不阻塞应用程序主线程的情况下执行多个并发操作的情况是有益的。

### Example: Asynchronous Insert with EF Core

### 示例：使用 EF Core 进行异步插入

```csharp
using System;
using Microsoft.EntityFrameworkCore;
using System.Threading.Tasks;

public class Program
{
    public static async Task Main()
    {
        using (var context = new BlogDbContext())
        {
            try
            {
                var newPost = new Post { Title = "New Post" };
                context.Posts.Add(newPost);
                await context.SaveChangesAsync();
Console.WriteLine("New post added with Id: " +
newPost.Id);
}
catch (Exception ex)
{
    Console.WriteLine("Error adding post: " +
ex.Message);
}
}
}
}
```

在这个示例中，`SaveChangesAsync` 用于将新帖子异步插入数据库。此操作异步执行以避免阻塞主线程。

## 4. Best Practices and Considerations:

## 4. 最佳实践和注意事项：

在利用 HttpClient 和 EF Core 等 .NET 库的异步功能时，遵循最佳实践并考虑某些方面至关重要：

- **Avoid Mixing Synchronous and Asynchronous Code:** Try to keep your codebase consistent with either synchronous or asynchronous patterns to avoid potential deadlocks and inefficiencies.
- **避免混合同步和异步代码：** 尝试让代码库保持同步或异步模式的一致性，以避免潜在的死锁和效率低下。
- **Use `await` Properly:** Always use the `await` keyword when calling asynchronous methods to ensure proper asynchronous behavior and avoid blocking.
- **正确使用 `await`：** 在调用异步方法时始终使用 `await` 关键字，以确保正确的异步行为并避免阻塞。
- **Handle Errors Gracefully:** Implement proper error handling and exception management strategies to handle asynchronous operation failures gracefully.
- **优雅地处理错误：** 实现适当的错误处理和异常管理策略，以优雅地处理异步操作失败。
- **Configure HttpClient Correctly:** When using HttpClient, configure it properly (such as setting timeout values) to avoid potential issues in production environments.
- **正确配置 HttpClient：** 使用 HttpClient 时，请正确配置它（例如设置超时值），以避免生产环境中的潜在问题。
- **Optimize Database Operations:** For database operations, consider optimizing queries, using proper indexing, and batching operations where applicable to improve performance.
- **优化数据库操作：** 对于数据库操作，请考虑优化查询、使用适当的索引以及在适用时批量操作以提高性能。

利用 HttpClient 和 Entity Framework Core 等 .NET 库的异步功能对于构建响应迅速、可扩展和高性能的应用程序至关重要。异步编程允许应用程序在不阻塞主线程的情况下高效地执行 I/O 绑定操作，从而提高用户体验和资源利用率。通过遵循最佳实践、优雅地处理错误以及优化数据库操作，开发人员可以充分发挥 .NET 应用程序中异步编程的全部潜力，确保最佳性能和响应能力。

# 第 6 章

# 第 6 章

### Designing responsive user interfaces (UIs) with asynchronous operations in WPF and Windows Forms

### 使用 WPF 和 Windows Forms 中的异步操作设计响应式用户界面 (UI)

设计响应式用户界面 (UI) 对于现代应用程序至关重要，尤其是在处理网络请求、数据库访问或长时间运行任务等异步操作时。在本次探索中，我们将讨论如何使用 C# 12 和 .NET 8 在 Windows Presentation Foundation (WPF) 和 Windows Forms 中使用异步操作设计响应式 UI。我们将介绍技术、最佳实践和代码示例，以演示 UI 应用程序中的异步编程。

### 1. Asynchronous Operations in WPF:

### 1. WPF 中的异步操作：

WPF 是一个功能强大的框架，用于构建具有丰富 UI 体验的桌面应用程序。WPF 中的异步编程可确保在长时间运行的任务或可能阻塞主线程的操作期间 UI 保持响应。

**Example**: Asynchronous Operation in WPF using async/await

**示例**：使用 async/await 在 WPF 中进行异步操作

```csharp
using System;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;

namespace WpfApp
{
public partial class MainWindow : Window
{
    public MainWindow()
    {
        InitializeComponent();
    }

    private async void Button_Click(object sender, RoutedEventArgs e)
    {
        // Disable button during operation
        button.IsEnabled = false;

        try
        {
            // Simulate a long-running operation
            await Task.Delay(3000); // Represents some asynchronous task

            // Update UI or perform further actions
            resultTextBlock.Text = "Operation completed";
        }
        catch (Exception ex)
        {
            // Handle exceptions
            resultTextBlock.Text = "Error: " + ex.Message;
        }
        finally
        {
            // Enable button after operation completes
            button.IsEnabled = true;
        }
    }
}
}
```

```csharp
{
    // Simulate a long-running operation
    await Task.Delay(3000); // Represents some asynchronous task

    // Update UI or perform further actions
    resultLabel.Text = "Operation completed";
}
catch (Exception ex)
{
    // Handle exceptions
    resultLabel.Text = "Error: " + ex.Message;
}
finally
{
    // Enable button after operation completes
    button.Enabled = true;
}
}
}
}
}
```

在这个 Windows Forms 示例中，`button_Click` 事件处理程序被标记为 `async` 以启用异步编程。与 WPF 示例类似，在异步操作（由 `Task.Delay` 模拟）执行期间，UI 保持响应。

### 3. Best Practices for Responsive UIs with Asynchronous Operations:

### 3. 异步操作响应式 UI 的最佳实践：

- **Use Asynchronous APIs:** Whenever possible, use asynchronous APIs for long-running or I/O-bound operations such as network requests, file operations, or database accesses. This prevents blocking the UI thread and ensures a responsive user experience.
- **使用异步 API：** 在可能的情况下，对于长时间运行或 I/O 绑定的操作（如网络请求、文件操作或数据库访问）使用异步 API。这可以防止阻塞 UI 线程并确保响应迅速的用户体验。
- **Disable UI Elements:** Disable UI elements (such as buttons) during long-running operations to prevent users from triggering multiple actions or interacting with elements that are not yet ready.
- **禁用 UI 元素：** 在长时间运行的操作期间禁用 UI 元素（如按钮），以防止用户触发多个操作或与尚未准备好的元素交互。
- **Handle Exceptions Gracefully:** Always handle exceptions in asynchronous operations to prevent crashes and provide meaningful error messages to users. Update the UI to inform the user about errors or unexpected behaviors.
- **优雅地处理异常：** 始终在异步操作中处理异常以防止崩溃并向用户提供有意义的错误消息。更新 UI 以告知用户错误或意外行为。
- **Update UI on UI Thread:** When updating UI elements from asynchronous operations, ensure that UI updates are performed on the UI thread. Use `Dispatcher.Invoke` (WPF) or `Control.Invoke` (WinForms) to marshal UI updates to the UI thread if needed.
- **在 UI 线程上更新 UI：** 从异步操作更新 UI 元素时，确保 UI 更新在 UI 线程上执行。如果需要，使用 `Dispatcher.Invoke`（WPF）或 `Control.Invoke`（WinForms）将 UI 更新封送到 UI 线程。
- **Use Progress Reporting:** For lengthy operations, consider implementing progress reporting to keep users informed about the progress of the operation. Use progress bars or status indicators to show progress visually.
- **使用进度报告：** 对于冗长的操作，请考虑实现进度报告以让用户了解操作的进度。使用进度条或状态指示器直观地显示进度。

使用 WPF 和 Windows Forms 中的异步操作设计响应式用户界面对于创建现代高效的桌面应用程序至关重要。通过利用 async/await、在操作期间禁用 UI 元素、优雅地处理异常、在 UI 线程上更新 UI 以及使用进度报告，开发人员可以在长时间运行或 I/O 绑定任务期间确保流畅且响应迅速的用户体验。使用 C# 12 和 .NET 8 的 UI 应用程序中的异步编程使开发人员能够构建健壮、高性能的桌面应用程序，以满足现代用户的期望。

## Handling UI updates and data binding within asynchronous contexts

## 在异步上下文中处理 UI 更新和数据绑定

在异步上下文中处理 UI 更新和数据绑定是现代应用程序开发的一个关键方面，尤其是在处理长时间运行的操作或异步任务时。在本次探索中，我们将讨论使用 C# 12 和 .NET 8 在异步上下文中处理 UI 更新和数据绑定的技术、最佳实践和代码示例。我们将重点关注 Windows Presentation Foundation (WPF) 和 Windows Forms 中异步操作与 UI 交互的场景。

### 1. Data Binding in WPF:

### 1. WPF 中的数据绑定：

WPF 提供了一个强大的数据绑定机制，允许 UI 元素根据底层数据源的变化自动更新。在处理异步操作时，确保由异步数据检索或处理触发的 UI 更新得到正确处理至关重要。

### Example: Asynchronous Data Binding in WPF

### 示例：WPF 中的异步数据绑定

让我们考虑一个 WPF 应用程序异步从远程源获取数据并显示数据的场景：

```csharp
using System;
using System.Collections.ObjectModel;
using System.ComponentModel;
using System.Threading.Tasks;
using System.Windows;
```




```csharp
namespace WpfApp
{
    public partial class MainWindow : Window, INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        private ObservableCollection<string> dataList;
        public ObservableCollection<string> DataList
        {
            get { return dataList; }
            set
            {
                dataList = value;
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(DataList)));
            }
        }

        public MainWindow()
        {
            InitializeComponent();
            DataContext = this;

            // Load data asynchronously
            LoadDataAsync();
        }

        private async void LoadDataAsync()
        {
            // Simulate data retrieval asynchronously
            await Task.Delay(3000); // Represents fetching data from a remote source

            // Update DataList property (bound to UI) with retrieved data
            DataList = new ObservableCollection<string> {
                "Item 1", "Item 2", "Item 3" };
        }
    }
}
```

在此示例中，`DataList` 是一个实现了 `INotifyPropertyChanged` 的属性，用于通知 UI 数据发生了变化。`LoadDataAsync` 方法模拟异步数据检索，并在数据准备好时更新 `DataList` 属性。由于数据绑定，UI 会自动反映这些更改。

## 2. 在 Windows Forms 中更新 UI 元素：

在 Windows Forms 应用程序中，在异步上下文中更新 UI 元素需要特别注意，以确保线程安全并避免跨线程问题。

**示例**：在 Windows Forms 中更新 UI 元素

```csharp
using System;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace WinFormsApp
{
    public partial class MainForm : Form
    {
        public MainForm()
        {
            InitializeComponent();
        }

        private async void button_Click(object sender, EventArgs e)
        {
            button.Enabled = false; // Disable button during operation

            // Simulate async operation
            await Task.Delay(3000); // Represents some asynchronous task

            // Update label text on UI thread
            Invoke((Action)(() => resultLabel.Text = "Operation completed"));

            button.Enabled = true; // Enable button after operation completes
        }
    }
}
```

在此示例中，使用 `Invoke` 将 UI 更新调度到 UI 线程。这是必要的，因为 Windows Forms 中的 UI 元素不是线程安全的，只能从 UI 线程访问。

## 3. 在异步上下文中处理 UI 更新的最佳实践：

- **使用 Dispatcher（WPF）或 Invoke（WinForms）：** 在 WPF 中，使用 `Dispatcher.Invoke` 或 `Dispatcher.BeginInvoke` 从非 UI 线程更新 UI 元素。在 Windows Forms 中，使用 `Control.Invoke` 或 `Control.BeginInvoke` 达到相同目的。
- **实现 INotifyPropertyChanged（WPF）：** 对于 WPF 中的数据绑定场景，在视图模型或数据上下文上实现 `INotifyPropertyChanged`，以通知 UI 属性更改。
- **正确处理跨线程访问（WinForms）：** 在 Windows Forms 中，确保使用 `Invoke` 或 `BeginInvoke` 在 UI 线程上执行 UI 更新，以防止跨线程异常。
- **正确使用 async/await：** 使用 async/await 时，确保在异步方法中正确处理 UI 更新和交互，以保持响应流畅的用户体验。

## 4. 复杂的 UI 更新和进度报告：

对于更复杂的 UI 更新或需要进度报告的场景（例如长时间运行的任务），请考虑使用进度条、状态指示器或专用进度窗口等额外 UI 元素，让用户随时了解当前操作的进度。

在异步上下文中处理 UI 更新和数据绑定对于构建响应迅速且用户友好的应用程序至关重要。无论是在 WPF 还是 Windows Forms 中，利用数据绑定、INotifyPropertyChanged、Dispatcher/Invoke 和 async/await 等机制，可确保 UI 元素在异步操作期间保持最新和响应。通过遵循最佳实践并理解使用 C# 12 和 .NET 8 在 UI 应用程序中进行异步编程的细微差别，开发人员可以创建现代高效的应用程序，提供无缝的用户体验。

## 为常见 UI 交互（例如按钮单击、数据加载）利用异步模式

在现代应用程序中，为常见 UI 交互利用异步模式对于构建响应迅速且高效的用户界面至关重要。异步编程使 UI 元素在数据加载、网络请求或复杂计算等长时间运行的任务期间保持响应。在本文中，我们将使用 C# 12 和 .NET 8 深入探讨如何为常见 UI 交互利用异步模式，并提供专注于 Windows Presentation Foundation (WPF) 和 Windows Forms 的代码示例。

### 1. 在 WPF 中异步处理按钮单击：

在 WPF 中，使用 async/await 异步处理按钮单击非常简单。这确保在后台执行耗时任务时 UI 保持响应。

### 示例：WPF 中的异步按钮单击

```csharp
using System;
using System.Threading.Tasks;
using System.Windows;

namespace WpfApp
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private async void Button_Click(object sender, RoutedEventArgs e)
        {
            button.IsEnabled = false; // Disable button during operation
            try
            {
                // Simulate async operation
                await Task.Delay(3000); // Represents some asynchronous task
                // Update UI or perform further actions
                resultTextBlock.Text = "Operation completed";
            }
            catch (Exception ex)
            {
                // Handle exceptions
                resultTextBlock.Text = "Error: " + ex.Message;
            }
            finally
            {
                button.IsEnabled = true; // Enable button after operation completes
            }
        }
    }
}
```

在此示例中，`Button_Click` 事件处理程序被标记为 `async`，允许我们在方法内使用 `await`。在异步操作期间按钮被禁用，以防止多次点击，同时 UI 保持响应。

### 2. 在 WPF 中异步加载数据：

在 UI 应用程序中，异步加载数据很常见，可以避免阻塞 UI 线程并确保流畅的用户交互。当从远程服务器获取数据或执行数据库查询时，通常会使用异步数据加载。

### 示例：WPF 中的异步数据加载

```csharp
using System;
using System.Collections.ObjectModel;
using System.ComponentModel;
using System.Threading.Tasks;
using System.Windows;

namespace WpfApp
{
    public partial class MainWindow : Window, INotifyPropertyChanged
    {
        public event PropertyChangedEventHandler PropertyChanged;

        private ObservableCollection<string> dataList;
        public ObservableCollection<string> DataList
        {
            get { return dataList; }
            set
            {
                dataList = value;
                PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(nameof(DataList)));
            }
        }

        public MainWindow()
        {
            InitializeComponent();
            DataContext = this;

            // Load data asynchronously
            LoadDataAsync();
        }

        private async void LoadDataAsync()
        {
            try
            {
                // Simulate data retrieval asynchronously
                await Task.Delay(3000); // Represents fetching data from a remote source

                // Update DataList property (bound to UI) with retrieved data
                DataList = new ObservableCollection<string> {
                    "Item 1", "Item 2", "Item 3" };
            }
            catch (Exception ex)
            {
                // Handle exceptions or show error message
                MessageBox.Show("Error loading data: " + ex.Message);
            }
        }
    }
}
```

在此示例中，在窗口初始化期间调用 `LoadDataAsync` 以异步加载数据。数据检索后更新 `DataList` 属性，UI 由于数据绑定自动反映更改。

### 3. 在 Windows Forms 中异步处理按钮单击：

同样，在 Windows Forms 应用程序中，可以使用 async/await 异步处理按钮单击，以确保 UI 具有响应。





```
button.Enabled = true; // Enable button after
operation completes
    }
  }
}
, ,
```

在此 Windows Forms 示例中，`button_Click` 事件处理程序被标记为 `async`，并在方法中使用 `await` 以异步方式处理按钮单击操作。

### 4. 异步 UI 交互的最佳实践：
- **禁用 UI 元素：** 在长时间运行的操作期间禁用 UI 元素，以防止多次点击，并确保用户不会与尚未就绪的元素进行交互。
- **处理异常：** 始终在异步方法中处理异常，以防止崩溃，并向用户提供有意义的错误消息或通知。
- **提供反馈：** 在异步操作期间，向用户提供反馈，例如进度条、状态消息或通知，让他们了解正在进行的进程。
- **使用异步方法：** 使用 async/await 方法进行异步操作，而不是同步阻塞方法，以保持 UI 的响应性。

在常见的 UI 交互中利用异步模式，对于构建响应迅速且用户友好的应用程序至关重要。无论是在 WPF 还是 Windows Forms 中，async/await 都使开发人员能够异步处理按钮点击、数据加载和其他操作，从而确保即使在长时间任务期间 UI 也能保持响应。
通过遵循最佳实践并理解使用 C# 12 和 .NET 8 在 UI 应用程序中进行异步编程的细微差别，开发人员可以创建现代高效的应用程序，提供无缝的用户体验。

# 第 7 章
## 使用 ASP.NET Core 8 构建响应迅速且可扩展的 Web 应用程序

构建响应迅速且可扩展的 Web 应用程序是现代软件开发的一个关键方面。ASP.NET Core 8 支持异步编程和异步模式，提供了强大的工具来创建既能响应用户交互又能高效处理并发请求的 Web 应用程序。在本节中，我们将深入探讨如何使用 ASP.NET Core 8 构建响应迅速且可扩展的 Web 应用程序，重点关注使用 C# 12 和 .NET 8 的异步编程技术。我们将涵盖异步控制器、异步数据库访问、异步 HTTP 请求，以及 ASP.NET Core 中处理异步操作的最佳实践。

### 1. ASP.NET Core 中的异步控制器：

ASP.NET Core 中的异步控制器允许异步处理 HTTP 请求，确保 Web 服务器保持响应，并能有效处理多个并发请求。

### 示例：异步控制器操作

```csharp
using Microsoft.AspNetCore.Mvc;
using System;
using System.Threading.Tasks;

namespace MyApp.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class UsersController : ControllerBase
    {
        [HttpGet("{id}")]
        public async Task<IActionResult> GetUserAsync(int id)
        {
            try
            {
                // Simulate asynchronous database access
                var user = await GetUserFromDatabaseAsync(id);

                if (user != null)
                {
                    return Ok(user);
                }
                else
                {
                    return NotFound();
                }
            }
            catch (Exception ex)
            {
                return StatusCode(500, "Internal server error");
            }
        }

        private async Task<User> GetUserFromDatabaseAsync(int id)
        {
            // Simulate database access asynchronously
            await Task.Delay(1000); // Represents fetching user data from the database

            // Return user or null if not found
            return null; // Simulated user data
        }
    }
}
```

```csharp
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    // Other user properties
}
```

在此示例中，`UsersController` 中的 `GetUserAsync` 操作是异步的，并使用 `await` 从数据库异步获取用户数据。这允许 Web 服务器在等待数据库操作完成时处理其他请求。

### 2. ASP.NET Core 中的异步数据库访问：

异步数据库访问对于构建可扩展的 Web 应用程序至关重要。ASP.NET Core 通过 Entity Framework Core (EF Core) 或其他 ORM 支持异步数据库操作，从而高效处理数据库查询和更新。

### 示例：使用 EF Core 进行异步数据库查询

```csharp
using Microsoft.AspNetCore.Mvc;
using MyApp.Data;
using System;
using System.Linq;
using System.Threading.Tasks;

namespace MyApp.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class ProductsController : ControllerBase
    {
        private readonly AppDbContext _context;
        public ProductsController(AppDbContext context)
        {
            _context = context;
        }
        [HttpGet]
        public async Task<IActionResult> GetProductsAsync()
        {
            try
            {
                var products = await _context.Products.ToListAsync();
                return Ok(products);
            }
            catch (Exception ex)
            {
                return StatusCode(500, "Internal server error");
            }
        }
    }
}
```

在此示例中，`ProductsController` 中的 `GetProductsAsync` 操作使用 EF Core 的 `ToListAsync` 方法从数据库异步获取产品。这确保了 Web 服务器在查询数据库时保持响应。

### 3. ASP.NET Core 中的异步 HTTP 请求：

ASP.NET Core 允许向外部 API 或服务发出异步 HTTP 请求，从而实现与外部系统的高效通信和集成。

**示例**：控制器中的异步 HTTP 请求

```csharp
using Microsoft.AspNetCore.Mvc;
using System.Net.Http;
using System.Threading.Tasks;

namespace MyApp.Controllers
{
    [ApiController]
    [Route("api/[controller]")]
    public class ExternalApiController : ControllerBase
    {
        private readonly HttpClient _httpClient;

        public ExternalApiController(HttpClient httpClient)
        {
            _httpClient = httpClient;
        }

        [HttpGet("external-data")]
        public async Task<IActionResult> GetExternalDataAsync()
        {
            try
            {
                var response = await _httpClient.GetAsync("https://api.example.com/data");
                response.EnsureSuccessStatusCode(); // Ensure success status code

                var data = await response.Content.ReadAsStringAsync();

                return Ok(data);
            }
            catch (Exception ex)
            {
```

根据需要设置值、连接池和其他设置。

- **使用依赖注入：** 在 ASP.NET Core 中，我更喜欢使用依赖注入将 DbContext、HttpClient 或其他依赖项注入到控制器或服务中。这有助于提高可测试性、模块化，并简化资源管理。

使用 ASP.NET Core 8 构建响应迅速且可扩展的 Web 应用程序需要有效利用异步编程技术。通过使用异步控制器、使用 EF Core 进行异步数据库访问，以及使用 HttpClient 发出异步 HTTP 请求，开发人员可以创建高效处理并发请求并保持响应式用户体验的应用程序。遵循正确的错误处理、HttpClient 配置以及使用依赖注入等最佳实践，对于提高代码的可维护性和性能至关重要。借助 C# 12 和 .NET 8，开发人员拥有强大的工具和框架，可以构建现代且高性能的 Web 应用程序。

## 高效处理异步 HTTP 请求和响应

高效处理异步 HTTP 请求和响应对于构建响应迅速且高性能的 Web 应用程序至关重要。在本节中，我们将深入探讨使用 C# 12 和 .NET 8 高效处理异步 HTTP 请求和响应的技术、最佳实践和代码示例，重点介绍 ASP.NET Core 中用于发出异步 HTTP 请求的 HttpClient 类。

### 1. 使用 HttpClient 发出异步 HTTP 请求：




ASP.NET Core 中的 HttpClient 类提供了强大的功能，可以异步地向外部 API 或服务发起 HTTP 请求。将 async/await 与 HttpClient 结合使用，可以确保应用程序在等待 HTTP 响应时保持响应。

## 示例：发起异步 GET 请求

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient httpClient = new HttpClient();

    public static async Task Main()
    {
        string url = "https://jsonplaceholder.typicode.com/posts/1";

        try
        {
            HttpResponseMessage response = await httpClient.GetAsync(url);
            response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)

            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine("Response from API:");
            Console.WriteLine(responseBody);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error fetching data: " + ex.Message);
        }
    }
}
```

在本例中，我们创建了一个静态 HttpClient 实例，向 JSONPlaceholder API 端点发起异步 GET 请求。`GetAsync` 方法返回一个 `Task<HttpResponseMessage>`，我们通过 await 异步接收 HTTP 响应。

## 2. 处理异步 HTTP 响应：

在发起异步 HTTP 请求后，高效地处理 HTTP 响应至关重要。这包括读取响应内容、检查状态码以及处理潜在异常。

**示例**：处理异步 HTTP 响应

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

public class Program
{
    private static readonly HttpClient httpClient = new HttpClient();

    public static async Task Main()
    {
        string url = "https://jsonplaceholder.typicode.com/posts/1";

        try
        {
            HttpResponseMessage response = await httpClient.GetAsync(url);
            response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)
            string responseBody = await response.Content.ReadAsStringAsync();
            Console.WriteLine("Response from API:");
            Console.WriteLine(responseBody);
            // Process response data further if needed
            // e.g., deserialize JSON response into objects
        }
        catch (HttpRequestException ex)
        {
            Console.WriteLine("HTTP Request Error: " + ex.Message);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error fetching data: " + ex.Message);
        }
    }
}
```

在本例中，我们使用 `EnsureSuccessStatusCode` 确保 HTTP 响应具有成功状态码（2xx）。然后，我们使用 `ReadAsStringAsync` 异步读取响应内容，并根据需要进一步处理数据，例如将 JSON 响应反序列化为对象。

## 3. 高效处理异步 HTTP 请求的最佳实践：

- **使用单个 HttpClient 实例：**创建单个 HttpClient 实例并全程复用

利用异步中间件和服务对于在 ASP.NET Core 应用程序中构建干净高效的架构至关重要。异步编程允许代码非阻塞执行，确保响应性和可扩展性，尤其是在 I/O 密集型场景（如数据库访问或外部 API 调用）中。在本文探讨中，我们将讨论如何使用 C# 12 和 .NET 8 在 ASP.NET Core 中利用异步中间件和服务来实现更干净的架构。我们将介绍异步中间件、异步服务、最佳实践以及代码示例来演示它们的用法。

## 1. ASP.NET Core 中的异步中间件：

ASP.NET Core 中的中间件是添加到 HTTP 请求管道中以处理请求和响应的软件组件。异步中间件可用于执行异步任务，例如日志记录、身份验证或请求/响应处理，而不会阻塞主线程。

### 示例：异步日志记录中间件

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
using System;
using System.Threading.Tasks;

public class LoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<LoggingMiddleware> _logger;

    public LoggingMiddleware(RequestDelegate next,
        ILogger<LoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation("Handling request: " + context.Request.Path);

        // Call the next middleware in the pipeline asynchronously
        await _next(context);

        _logger.LogInformation("Completed request: " + context.Request.Path);
    }
}

public static class LoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseLoggingMiddleware(this IApplicationBuilder builder)
    {
        return builder.UseMiddleware<LoggingMiddleware>();
    }
}
```

在本例中，我们创建了一个异步日志记录中间件，在处理每个 HTTP 请求之前和之后记录信息。`InvokeAsync` 方法是异步的，允许它在不阻塞请求管道的情况下执行日志记录任务。

## 2. ASP.NET Core 中的异步服务：

ASP.NET Core 中的服务用于业务逻辑、数据访问或其他应用程序特定功能。异步服务对于涉及 I/O 密集型任务（如数据库查询或外部 API 调用）的操作非常有用。

### 示例：异步 DataService

```csharp
using System.Collections.Generic;
using System.Threading.Tasks;

public interface IDataService
{
    Task<List<string>> GetItemsAsync();
}

public class DataService : IDataService
{
    public async Task<List<string>> GetItemsAsync()
    {
        // Simulate asynchronous data retrieval (e.g., from a database)
        await Task.Delay(1000); // Represents database query or API call

        // Return data as a list of strings
        return new List<string> { "Item 1", "Item 2", "Item 3" };
    }
}
```

在本例中，我们定义了一个异步 `IDataService` 接口，其方法 `GetItemsAsync` 异步返回字符串列表。`DataService` 类实现了该接口，并提供了异步获取项的实际实现。

## 3. 利用异步中间件和服务的最佳实践：

- **各处使用 Async/Await：**在中间件、服务和控制器操作中始终如一地使用 async/await 模式，以确保非阻塞执行和响应能力。
- **为服务实现接口：**为服务定义接口，并使用依赖注入将服务注入到控制器或其他组件中。这可以提升模块化、可测试性和可维护性。
- **优雅地处理错误：**在异步中间件和服务中实现适当的错误处理和异常管理，以处理异常并向客户端提供有意义的错误消息。
- **优化异步任务：**通过配置超时值、使用取消令牌以及避免不必要的阻塞操作来优化异步任务，以提高性能和资源利用率。
- **测试异步代码：**为异步中间件和服务编写单元测试，以确保它们在不同场景下的正确性、性能和行为。

## 4. 在 ASP.NET Core 应用程序中使用异步中间件和服务：

### 在 Startup.cs 中配置中间件

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddScoped<IDataService, DataService>();

        // Add other services
    }

    public void Configure(IApplicationBuilder app,
        IWebHostEnvironment env)
    {
        app.UseLoggingMiddleware();

        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }

        app.UseHttpsRedirection();
        app.UseRouting();
        app.UseAuthorization();

        app.UseEndpoints(endpoints =>
        {
            endpoints.MapControllers();
        });
    }
}
```

在 Startup.cs 的 `ConfigureServices` 方法中，我们使用依赖注入将 DataService 注册为作用域服务。在 `Configure` 方法中，我们使用 `UseLoggingMiddleware` 扩展方法添加异步日志记录中间件，然后添加其他用于路由、授权和端点映射的中间件。

利用异步中间件和服务对于在 ASP.NET Core 应用程序中构建干净、高效和可扩展的架构至关重要。通过利用异步编程技术（如 async/await、依赖注入和适当的错误

通过异步处理，开发人员可以创建异步处理 I/O 密集型操作的应用程序，确保响应性和性能。异步中间件支持非阻塞请求处理，而异步服务则能实现高效的数据访问和业务逻辑执行。借助 C# 12 和 .NET 8，开发人员拥有强大的工具和框架来有效实施异步模式，从而在 ASP.NET Core 应用程序中实现更简洁、更易维护的代码库。

## 探索 `IAsyncEnumerable` 等功能以处理 Web 应用程序中的大型数据流

探索 `IAsyncEnumerable` 等功能以处理 Web 应用程序中的大型数据流，对于提高资源利用率和改进响应性至关重要。`IAsyncEnumerable` 允许开发人员异步处理数据序列，这在处理大型数据集或数据检索涉及数据库查询或网络请求等异步操作时非常有用。在本次探索中，我们将深入介绍 `IAsyncEnumerable`、其优点、在 Web 应用程序中的用法，并提供基于 C# 12 和 .NET 8 异步编程的代码示例。

### 理解 `IAsyncEnumerable`：

`IAsyncEnumerable` 是在 C# 8.0 和 .NET Core 3.0 中引入的接口，表示数据元素的异步序列。它是 System.Collections.Generic 命名空间的一部分，旨在与异步操作无缝协作，允许在数据可用时进行处理，而无需等待整个数据集加载到内存中。

### `IAsyncEnumerable` 的优点：

- **高效的内存使用：** `IAsyncEnumerable` 可以处理大型数据集，而无需一次性将所有数据加载到内存中，这有利于高效处理大型数据流。
- **非阻塞：** 异步流允许非阻塞数据处理，确保在异步检索或处理数据时应用程序保持响应。
- **流式数据：** 应用程序可以实时或按块流式传输数据，从而减少延迟并提高整体性能，尤其是在处理大量数据的 Web 应用程序中。

### 在 Web 应用程序中使用 `IAsyncEnumerable`：

**示例 1：** Web API 控制器中的异步数据检索

```csharp
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;

[ApiController]
[Route("api/[controller]")]
public class DataController : ControllerBase
{
    [HttpGet]
    public async IAsyncEnumerable<string> GetDataAsync()
    {
        var dataStream = GetDataStreamAsync(); // Asynchronously retrieve data stream

        // Enumerate and return data asynchronously
        await foreach (var item in dataStream)
```

```csharp
public class Program
{
    private static readonly HttpClient httpClient = new HttpClient();
    public static async Task Main()
    {
        string url = "https://localhost:5001/api/data";
        try
        {
            HttpResponseMessage response = await httpClient.GetAsync(url);
            response.EnsureSuccessStatusCode(); // Ensure success status code (2xx)
            await foreach (var item in response.Content.ReadAsAsync<IEnumerable<string>>())
            {
                Console.WriteLine(item); // Process each item asynchronously
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine("Error fetching data: " + ex.Message);
        }
    }
}
```

在这个客户端示例中，应用程序向 `DataController` 端点发起异步 HTTP GET 请求，该端点返回异步数据序列。`await foreach` 循环会在数据流中的每个数据项可用时异步处理它们。

### 使用 `IAsyncEnumerable` 的最佳实践：

- **异步数据检索：** 使用 `IAsyncEnumerable` 进行异步数据检索操作，如数据库查询、文件 I/O 或外部 API 调用，以高效处理大型数据流。
- **流处理：** 利用异步流处理技术（如 `await foreach`）在数据元素生成时异步处理它们。
- **释放资源：** 使用异步流时，确保正确释放资源和进行清理，以避免资源泄漏。
- **错误处理：** 为异步流实现错误处理和异常管理，以优雅地处理异常并提供有意义的错误消息。

`IAsyncEnumerable` 是 C# 和 .NET 中一个强大的功能，它使开发人员能够有效地处理 Web 应用程序中的大型数据流。通过利用异步编程技术和异步流，应用程序可以异步处理数据，从而提高响应性、可扩展性和资源利用率。无论在 ASP.NET Core 控制器、客户端应用程序还是其他组件中，`IAsyncEnumerable` 都提供了一种简洁高效的方式来处理异步数据流和大型数据集，而不会阻塞应用程序的主线程。将 `IAsyncEnumerable` 纳入你的架构，可以在 C# 12 和 .NET 8 的异步编程范式中构建响应更快、可扩展性更强的 Web 应用程序。

```csharp
{
    private readonly MyService _service;

    public MyFunction(MyService service)
    {
        _service = service;
    }

    [Function("MyAsyncFunction")]
    public async Task<IActionResult> RunAsync(
        [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequestData req,
        FunctionContext context)
    {
        var logger = context.GetLogger<MyFunction>();
        logger.LogInformation("C# HTTP trigger function processed a request.");

        // Perform asynchronous operation using MyService
        var result = await _service.PerformAsyncOperation();

        return new OkObjectResult(result);
    }
}

public class MyService
{
    public async Task<string> PerformAsyncOperation()
    {
        // Simulate asynchronous operation
        await Task.Delay(1000); // Represents an asynchronous task

        return "Async operation completed";
    }
}
```

在此示例中，`MyAsyncFunction` 是由 HTTP 请求触发的异步 Azure Function。它使用依赖注入来注入 `MyService`，该服务执行异步操作（`PerformAsyncOperation`）。异步编程使函数能够在等待异步操作完成的同时处理其他请求。

## 2. AWS Lambda 中的异步编程：

AWS Lambda 是 Amazon Web Services (AWS) 提供的无服务器计算服务，允许开发人员在不管理服务器的情况下运行代码以响应事件。与 Azure Functions 类似，AWS Lambda 支持异步编程来处理并发请求和执行非阻塞操作。

**示例**：异步 AWS Lambda 函数（使用 AWS SDK for .NET）

```csharp
using System;
using Amazon.Lambda.Core;
using Amazon.Lambda.APIGatewayEvents;
using Amazon.Lambda.Serialization.SystemTextJson;
using Amazon.Lambda.S3Events;

public class MyLambdaFunction
{
    private readonly IAmazonS3 _s3Client;
    public MyLambdaFunction()
    {
        _s3Client = new AmazonS3Client();
    }

    [LambdaSerializer(typeof(DefaultLambdaJsonSerializer))]
    // Use JSON serialization

    public async Task<string> MyAsyncLambdaFunction(APIGatewayProxyRequest request, ILambdaContext context)
    {
        context.Logger.LogLine("Processing request...");

        // Perform asynchronous operation using AWS SDK for .NET (e.g., S3 operation)
        var response = await _s3Client.GetObjectAsync("my-bucket", "my-object-key");

        return $"Async operation completed. Content length: {response.ContentLength}";
    }
}
```

在此示例中，`MyAsyncLambdaFunction` 是由 API Gateway 代理请求触发的异步 AWS Lambda 函数。该函数使用 AWS SDK for .NET（Amazon.S3 命名空间）执行异步操作（`GetObjectAsync`），以从 S3 存储桶中检索对象。异步编程允许 Lambda 函数在等待 S3 操作完成的同时处理其他请求。

## 与云服务进行异步集成的最佳实践：

- **使用异步 SDK：** 利用云服务 SDK（例如 Azure SDK for .NET、AWS SDK for .NET）提供的异步 API 来高效执行异步操作。
- **优化资源使用：** 利用异步编程来减少资源消耗并提高可扩展性，尤其是在 Azure Functions 和 AWS Lambda 等无服务器环境中。



**3. 错误处理：** 为异步操作实现适当的错误处理和重试机制，以处理瞬态错误并确保健壮性。

**4. 监控性能：** 监控和分析异步操作的性能，以识别瓶颈、优化资源利用率并提高整体系统性能。

利用异步编程实现与 Azure Functions 和 AWS Lambda 等云服务的有效集成，对于构建现代、可扩展且响应迅速的云原生应用程序至关重要。通过利用 async/await 模式、异步 API 和最佳实践，开发人员可以设计无服务器函数和应用程序，以处理并发请求、执行非阻塞 I/O 操作并优化云环境中的资源使用。C# 12 和 .NET 8 中的异步编程为构建在当今云计算环境中可扩展、弹性且具有成本效益的云原生应用程序提供了强大的功能。

## 构建用于事件驱动架构的异步无服务器函数

构建用于事件驱动架构的异步无服务器函数是现代云原生应用程序的关键方面。像 Azure Functions、AWS Lambda 和 Google Cloud Functions 这样的无服务器计算平台提供了一种可扩展且具有成本效益的方式来响应事件执行代码，而无需管理服务器。

异步编程在开发高效且响应迅速的无服务器函数中发挥着至关重要的作用，特别是在事件驱动架构中，多个事件可以触发并发执行。在本探索中，我们将深入研究使用 C# 12 和 .NET 8 构建异步无服务器函数，重点关注 Azure Functions 和 AWS Lambda，包括代码示例和最佳实践。

### 1. Azure Functions 中的异步无服务器函数：

Azure Functions 是 Microsoft Azure 提供的无服务器计算服务，允许开发人员使用包括 C# 在内的各种编程语言编写事件驱动代码。异步编程在 Azure Functions 中被广泛用于高效处理数据库查询、外部 API 调用和长时间运行任务等异步操作。

### 示例：由 Blob 存储事件触发的异步 Azure 函数

```csharp
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System.IO;
using System.Threading.Tasks;

public static class BlobTriggerFunction
{
    [FunctionName("BlobTriggerFunction")]
    public static async Task RunAsync(
        [BlobTrigger("my-container/{name}", Connection = "AzureWebJobsStorage")] Stream blobStream,
        string name,
        ILogger log)
    {
        log.LogInformation($"Blob trigger function processed blob: {name}");

        // Asynchronous processing of blob content
        await ProcessBlobAsync(blobStream);
        log.LogInformation($"Blob processing completed for: {name}");
    }
    private static async Task ProcessBlobAsync(Stream blobStream)
    {
        // Simulate asynchronous processing of blob content
        using (StreamReader reader = new StreamReader(blobStream))
        {
            string content = await reader.ReadToEndAsync();
            // Process content asynchronously (e.g., store in database, send to external API)
        }
    }
}
```

在此示例中，`BlobTriggerFunction` 是一个由 Blob 存储事件触发的异步 Azure 函数。该函数使用 `Stream` 作为输入绑定来异步处理 Blob 内容。`ProcessBlobAsync` 方法模拟了 Blob 内容的异步处理，例如将其存储到数据库或发送到外部 API。

### 2. AWS Lambda 中的异步无服务器函数：

AWS Lambda 是 Amazon Web Services (AWS) 提供的无服务器计算服务，允许开发人员在无需配置或管理服务器的情况下响应事件运行代码。异步编程对于 AWS Lambda 处理并发请求和高效执行非阻塞 I/O 操作至关重要。

### 示例：处理 S3 事件的异步 AWS Lambda 函数

```csharp
using Amazon.Lambda.Core;
using Amazon.Lambda.S3Events;
using Amazon.S3;
using Amazon.S3.Util;
using System.Threading.Tasks;

public class S3EventProcessor
{
    private readonly IAmazonS3 _s3Client;
    public S3EventProcessor()
    {
        _s3Client = new AmazonS3Client();
    }

    public async Task ProcessS3EventAsync(S3Event s3Event, ILambdaContext context)
    {
        context.Logger.LogLine("Processing S3 event...");
        foreach (var record in s3Event.Records)
        {
            var response = await _s3Client.GetObjectAsync(record.S3.Bucket.Name, record.S3.Object.Key);
            // Process S3 object content asynchronously
        }
        context.Logger.LogLine("S3 event processing completed.");
    }
}
```

在此 AWS Lambda 示例中，`ProcessS3EventAsync` 是一个异步方法，用于处理由 S3 存储桶中的对象创建、删除或修改触发的 S3 事件。该方法使用 AWS SDK for .NET（`Amazon.S3` 命名空间）与 S3 交互并异步处理对象内容。

### 构建异步无服务器函数的最佳实践：

- 1. **使用 Async/Await：** 利用 async/await 关键字进行异步编程，以处理 I/O 密集型操作并提高并发性。
- 2. **优化资源使用：** 通过使用异步操作并及时释放资源来最小化资源使用，以提高可扩展性并降低成本。
- 3. **错误处理：** 为异步操作实现适当的错误处理和重试机制，以处理瞬态错误并确保可靠性。
- 4. **依赖注入：** 使用依赖注入将服务或依赖项注入到无服务器函数中，以获得更好的模块化、可测试性和可维护性。
- 5. **监控性能：** 监控和分析异步无服务器函数的性能，以识别瓶颈、优化执行时间并提高整体系统性能。

用于事件驱动架构的异步无服务器函数对于开发可扩展、响应迅速且具有成本效益的云原生应用程序至关重要。使用 C# 12 和 .NET 8 的异步编程使开发人员能够在 Azure Functions 和 AWS Lambda 等无服务器计算环境中处理并发请求、执行非阻塞 I/O 操作并优化资源使用。通过遵循最佳实践、利用 async/await 模式以及有效使用云提供商 SDK，开发人员可以创建高效可靠的无服务器函数，使其无缝集成到事件驱动架构中，并在云中提供高性能解决方案。

## 为云消息传递和分布式系统实现异步通信模式

实现云消息传递和分布式系统的异步通信模式对于在现代云环境中构建可扩展、响应迅速且容错的应用程序至关重要。异步通信模式允许系统通过利用非阻塞 I/O 操作来处理并发请求、解耦组件并提高整体系统性能。在本探索中，我们将深入研究使用 C# 12 和 .NET 8 实现异步通信模式，重点关注使用 Azure Service Bus 的云消息传递和分布式系统通信，包括代码示例和最佳实践。

### 1. 云消息传递中的异步通信模式：

诸如 Azure Service Bus、AWS SQS（Simple Queue Service）和 Google Cloud Pub/Sub 之类的云消息传递服务为解耦组件并在分布式系统中实现可靠的消息处理提供了异步通信功能。

### 示例：使用 Azure Service Bus 的异步消息接收器

```csharp
using Azure.Messaging.ServiceBus;
using System;
using System.Threading.Tasks;

public class MessageReceiver
{
    private readonly string _connectionString;
    private readonly string _queueName;

    public MessageReceiver(string connectionString, string queueName)
    {
        _connectionString = connectionString;
        _queueName = queueName;
    }

    public async Task ReceiveMessagesAsync()
    {
        await using var client = new ServiceBusClient(_connectionString);
        var receiver = client.CreateReceiver(_queueName);

        while (true)
        {
            ServiceBusReceivedMessage message = await receiver.ReceiveMessageAsync();

            if (message != null)
            {
                Console.WriteLine($"Received message: {message.Body}");
                await receiver.CompleteMessageAsync(message);
            }
            else
            {
                break; // No more messages available
            }
        }
    }
}
```



在本示例中，`MessageReceiver` 是一个演示如何使用 Azure Service Bus 进行异步消息接收的类。它连接到 Service Bus 队列，持续异步接收消息，处理消息并在完成后将消息标记为完成。

## 2. 分布式系统中的异步通信：

在分布式系统中，异步通信模式（如事件驱动消息传递、异步 RPC（远程过程调用）和消息队列）用于实现微服务之间的通信、处理大规模工作负载并确保容错能力。

**示例**：使用 gRPC 和 .NET 实现异步 RPC

```csharp
using Grpc.Core;
using System.Threading.Tasks;

// Define gRPC service contract and methods
public interface IMyService
{
    Task<MyResponse> MyMethodAsync(MyRequest request);
}

public class MyService : IMyService
{
    public async Task<MyResponse> MyMethodAsync(MyRequest request)
    {
        // Simulate asynchronous processing
        await Task.Delay(1000); // Represents an async operation
        return new MyResponse { Result = "Processed result" };
    }
}

// Server implementation
public class MyServiceServer
{
    private readonly Server _server;

    public MyServiceServer()
    {
        _server = new Server
        {
            Services = { MyService.BindService(new MyService()) },
            Ports = { new ServerPort("localhost", 5000, ServerCredentials.Insecure) }
        };
    }

    public void Start()
    {
        _server.Start();
    }

    public async Task ShutdownAsync()
    {
        await _server.ShutdownAsync();
    }
}
```

在此示例中，我们定义了一个包含异步方法（`MyMethodAsync`）的 gRPC 服务（`IMyService`），并在 `MyService` 中实现了服务逻辑。`MyServiceServer` 类创建并启动一个 gRPC 服务器，用于处理来自客户端的传入异步 RPC 请求。

实现高效的异步通信模式，并构建满足当今基于云的架构需求的分布式系统。

# 第 9 章

## 异步代码的有效测试策略

### 理解测试异步代码的挑战

理解测试异步代码的挑战对于确保严重依赖异步编程模式（如 async/await）的应用程序的正确性、可靠性和性能至关重要。异步代码引入了与时间、并发和非确定性行为相关的复杂性，这使得与同步代码相比，测试更具挑战性。在本次探讨中，我们将深入探讨使用 C# 12 和 .NET 8 测试异步代码的挑战，讨论克服这些挑战的策略，并在适用时提供代码示例。

### 1. 测试异步代码的挑战：

- **时间依赖**：异步代码会引入时间依赖，其中异步操作的完成可能会因系统负载、网络延迟或外部因素而有所不同。测试依赖于特定时序的代码可能会导致测试不稳定或不确定。

- **并发问题**：如果处理不当，异步代码中的并发可能导致竞态条件、死锁或状态不一致问题。测试并发代码需要仔细的同步和协调，以确保在并发执行下行为正确。

- **模拟异步依赖**：由于 async/await 模式的性质，模拟异步依赖（如异步方法、返回 Task 的方法或外部 API）可能具有挑战性。模拟框架需要支持异步行为和可等待类型。

- **错误处理和异常**：测试异步代码中的错误处理和异常路径需要模拟不同的错误场景，确保正确的异常传播，并验证错误处理逻辑。

- **测试异步数据流**：测试使用异步数据流（例如 IAsyncEnumerable、事件流）的代码需要处理异步迭代、缓冲和按到达顺序处理数据，这增加了测试设置的复杂性。

### 2. 克服挑战的策略：

- **在测试中使用 Async/Await**：在测试方法中利用 async/await 关键字来编写异步测试代码，以模拟被测代码的异步行为。这允许测试等待异步操作完成并验证结果。

- **支持异步的模拟框架**：使用支持异步模拟和可等待类型的模拟框架。流行的模拟框架（如 Moq、NSubstitute 和 FakeItEasy）支持模拟异步方法并处理测试中的异步行为。

- **使用 TaskCompletionSource 进行控制**：对于具有自定义异步行为或依赖项的异步方法测试，请使用 `TaskCompletionSource` 创建可等待的任务并控制其完成，从而精确测试异步流程。

- **使用 Task.WhenAll 等待并行执行**：在测试涉及并行异步操作的场景时，使用 `Task.WhenAll` 并发等待多个任务，并确保在断言结果或继续测试逻辑之前所有任务都已完成。

- **考虑使用异步测试库**：探索专门设计用于测试异步代码的库，例如 `Microsoft.VisualStudio.Threading.AsyncTesting` 包，它提供了用于测试异步代码和在单元测试中管理异步上下文的工具。

### 3. 示例：使用 xUnit 和 Moq 测试异步方法：

让我们考虑一个使用 xUnit 进行单元测试、使用 Moq 模拟依赖项来测试异步方法的示例。

```csharp
public interface IDataService
{
    Task<int> GetDataAsync();
}

public class MyService
{
    private readonly IDataService _dataService;

    public MyService(IDataService dataService)
    {
        _dataService = dataService;
    }
    public async Task<int> ProcessDataAsync()
    {
        int data = await _dataService.GetDataAsync();
        // Process data asynchronously
        return data * 2; // Example processing logic
    }
}
public class MyServiceTests
{
    [Fact]
    public async Task ProcessDataAsync_ReturnsProcessedValue()
    {
        // Arrange
        int fakeData = 42;
        var mockDataService = new Mock<IDataService>();
        mockDataService.Setup(d => d.GetDataAsync()).ReturnsAsync(fakeData);

        var myService = new MyService(mockDataService.Object);

        // Act
        int result = await myService.ProcessDataAsync();

        // Assert
        Assert.Equal(84, result); // Expected processed value
        mockDataService.Verify(d => d.GetDataAsync(), Times.Once); // Verify data service call
    }
}
```

在此示例中，我们有一个依赖于 `IDataService` 进行异步数据检索的 `MyService` 类。我们使用 Moq 模拟 `IDataService`，并提供一个假数据值来测试 `ProcessDataAsync` 方法的处理逻辑。测试方法使用 async/await 来测试 `ProcessDataAsync` 的异步行为并断言预期结果。

由于时间依赖、并发问题、模拟异步依赖、错误处理和测试异步数据流，测试异步代码带来了独特的挑战。然而，通过正确的策略和工具，开发人员可以有效地测试异步代码，并确保其正确性、可靠性和性能。在测试中利用 async/await、使用支持异步的模拟框架、使用 `TaskCompletionSource` 控制异步行为以及考虑异步测试库，是在 C# 12 和 .NET 8 中成功测试异步代码的基本实践。通过主动应对这些挑战，开发人员可以构建健壮且可维护的异步代码库，并对其测试覆盖率充满信心。

## 利用单元测试框架（例如 xUnit、NUnit）进行异步场景测试

利用 xUnit 和 NUnit 等单元测试框架进行异步场景测试，对于确保 C# 12 和 .NET 8 中异步代码的正确性、可靠性和性能至关重要。单元测试框架提供了专门用于处理异步代码的功能和断言，使开发人员能够编写模拟异步行为并验证预期结果的测试。在本次探讨中，我们将深入探讨如何使用 xUnit 和 NUnit 测试异步场景，包括代码示例和最佳实践。

### 1. 使用 xUnit 对异步方法进行单元测试：

xUnit 是一个流行的用于 .NET 应用的单元测试框架，提供了编写和执行单元测试的丰富功能。它完全支持使用 async/await 测试异步方法，并为异步场景提供内置断言。

## **示例：** 使用 xUnit 测试异步方法

让我们考虑一个使用 xUnit 进行单元测试的异步方法测试示例。

```csharp
public class MyService
{
    public async Task<int> GetDataAsync()
    {
        // Simulate asynchronous data retrieval
        await Task.Delay(100); // Represents an asynchronous task

        return 42; // Example data
    }
}
public class MyServiceTests
{
    [Fact]
    public async Task GetDataAsync_ReturnsData()
    {
        // Arrange
        var myService = new MyService();

        // Act
        int result = await myService.GetDataAsync();

        // Assert
        Assert.Equal(42, result); // Verify expected result
    }
}
```

在此示例中，我们有一个 `MyService` 类，其中包含一个异步方法 `GetDataAsync`，用于模拟异步数据检索。`MyServiceTests` 类使用 xUnit 的 `[Fact]` 属性为测试方法断言调用 `GetDataAsync` 的预期结果。

## 2. 使用 NUnit 进行异步方法单元测试：

**示例**：使用 NUnit 测试异步方法

让我们使用 NUnit 重写之前的示例以测试异步方法。

```csharp
public class MyService
{
    public async Task<int> GetDataAsync()
    {
        // Simulate asynchronous data retrieval
        await Task.Delay(100); // Represents an asynchronous task
        return 42; // Example data
    }
}

[TestFixture]
public class MyServiceTests
{
    [Test]
    public async Task GetDataAsync_ReturnsData()
    {
        // Arrange
        var myService = new MyService();

        // Act
        int result = await myService.GetDataAsync();

        // Assert
        Assert.AreEqual(42, result); // Verify expected result
    }
}
```

在此 NUnit 示例中，我们使用 `[TestFixture]` 和 `[Test]` 属性分别定义测试夹具和测试方法。async/await 模式用于测试 `GetDataAsync` 的异步行为，并使用 NUnit 的断言方法断言预期结果。

## 测试异步场景的最佳实践：

- 1. **使用 Async/Await：** 在测试方法中利用 async/await 关键字处理异步代码并等待异步操作完成。
- 2. **使用异步测试方法：** 在测试异步代码时将测试方法定义为 async，以启用异步执行并等待异步操作。
- 3. **断言异步结果：** 使用单元测试框架提供的适当断言方法（例如，`Assert.Equal`、`Assert.IsTrue`）来验证异步操作的预期结果。
- 4. **测试异常路径：** 通过使用 try/catch 块或针对异常的特定断言方法（例如 xUnit 中的 `Assert.ThrowsAsync`）编写测试以覆盖异步方法中的错误处理和异常路径。
- 5. **考虑异步设置和拆卸：** 如有需要，在测试夹具中使用异步设置（`SetUpAsync`）和拆卸（`TearDownAsync`）方法来执行异步设置或清理操作。

单元测试框架如 xUnit 和 NUnit 为 C# 12 和 .NET 8 应用中的异步场景测试提供了出色的支持。通过利用 async/await 模式、异步测试方法和适当的断言方法，开发人员可以为异步代码编写有效的单元测试以确保其正确性和可靠性。无论是测试异步方法、处理异步异常还是验证异步行为，xUnit 和 NUnit 都提供了强大的功能和最佳实践，可自信地测试异步场景。将这些实践纳入单元测试策略有助于保持代码质量、及早发现错误并提高异步编程范式中软件的整体可靠性。

## 模拟异步依赖项和异步行为

模拟异步依赖项和异步行为是使用 C# 12 和 .NET 8 进行异步编程时单元测试的重要方面。模拟允许开发人员通过用模拟对象替换真实依赖项来隔离被测代码，而模拟异步行为则能够测试异步方法、任务和异步流程。在本次探索中，我们将深入探讨使用流行的模拟框架如 Moq 和 NUnit 以及 C# 12 和 .NET 8 来模拟异步依赖项和异步行为，包括代码示例和最佳实践。

### 1. 使用 Moq 模拟异步依赖项：

Moq 是一个流行的 .NET 模拟库，允许开发人员创建模拟对象、设置期望，并

```csharp
using Moq;
using Xunit;

public class MyServiceTests
{
    [Fact]
    public async Task ProcessDataAsync_ReturnsProcessedValue()
    {
        // Arrange
        var mockDataService = new Mock<IDataService>();
        mockDataService.Setup(d =>
        d.GetDataAsync()).ReturnsAsync(42); // Setup mock behavior

        var myService = new MyService(mockDataService.Object);

        // Act
        int result = await myService.ProcessDataAsync();

        // Assert
        Assert.Equal(84, result); // Expected processed value
        mockDataService.Verify(d => d.GetDataAsync(),
        Times.Once); // Verify data service call
    }
}
```

在此示例中，我们使用 Moq 创建 `IDataService` 的模拟实例，并使用 `ReturnsAsync` 设置其行为，以便在调用 `GetDataAsync` 时异步返回预定义的值。测试验证 `ProcessDataAsync` 方法是否正确处理从模拟数据服务获取的数据。

### 2. 使用 NUnit 模拟异步行为：

虽然 NUnit 主要是一个单元测试框架，但它可以与 Moq 等模拟库结合使用，以模拟异步行为并有效测试异步方法。

### **示例**：使用 NUnit 与 Moq 模拟异步行为

让我们扩展之前的示例并模拟 `GetDataAsync` 需要一些时间异步完成的情况。

```csharp
public interface IDataService
{
    Task<int> GetDataAsync();
}

public class MyService
{
    private readonly IDataService _dataService;

    public MyService(IDataService dataService)
    {
        _dataService = dataService;
    }

    public async Task<int> ProcessDataAsync()
    {
        int data = await _dataService.GetDataAsync();
        // Process data asynchronously
        return data * 2; // Example processing logic
    }
}
```

现在，让我们使用 NUnit 和 Moq 编写一个单元测试来模拟 `GetDataAsync` 的异步行为。

```csharp
using Moq;
using NUnit.Framework;
using System.Threading.Tasks;

[TestFixture]
public class MyServiceTests
{
    [Test]
    public async Task ProcessDataAsync_ReturnsProcessedValue()
    {
        // Arrange
        var mockDataService = new Mock<IDataService>();
        mockDataService.Setup(d =>
            d.GetDataAsync()).Returns(async () =>
        {
            await Task.Delay(100); // Simulate async delay
            return 42;
        });

        var myService = new MyService(mockDataService.Object);

        // Act
        int result = await myService.ProcessDataAsync();

        // Assert
        Assert.AreEqual(84, result); // Expected processed value
        mockDataService.Verify(d => d.GetDataAsync(),
            Times.Once); // Verify data service call
    }
}
```

在此 NUnit 示例中，我们使用 Moq 通过使用来设置 `GetDataAsync` 的异步行为

`Returns` 与一个异步 lambda 一起使用，该 lambda 在返回值之前模拟延迟。这模拟了数据服务的异步特性，使我们能够有效地测试 `ProcessDataAsync` 中的异步处理。

## 模拟异步依赖和模拟异步行为的最佳实践：

- 1. **使用模拟库：** 利用支持模拟异步方法和任务的模拟库，如 Moq、NSubstitute 或 FakeItEasy。
- 2. **设置异步行为：** 使用 `ReturnsAsync`（Moq）或带异步 lambda 的 `Returns`（Moq/NUnit）来设置被模拟方法或任务的异步行为。
- 3. **验证异步调用：** 使用模拟框架提供的 `Verify` 或类似方法来验证异步方法调用及其调用次数。
- 4. **模拟延迟和错误：** 在模拟设置中模拟异步延迟或错误场景，以测试被测代码中的错误处理和异步行为。
- 5. **使用异步测试方法：** 在测试异步代码时，将测试方法定义为 async，以便等待异步操作并确保正确的异步执行。

模拟异步依赖和模拟异步行为是在 C# 12 和 .NET 8 中对异步代码进行单元测试的基本技术。通过使用如 Moq 等模拟库并利用异步设置功能，开发人员可以隔离被测代码、模拟依赖项的异步行为并有效验证异步交互。将这些最佳实践纳入单元测试策略，可确保对异步方法、任务和异步流程进行全面测试，从而在现代 C# 和 .NET 应用程序中实现更可靠、更健壮的异步代码库。

## 编写清晰且可维护的异步单元测试的最佳实践

编写清晰且可维护的异步单元测试，对于确保在 C# 12 和 .NET 8 中严重依赖异步编程的代码库的可靠性、正确性和可读性至关重要。异步单元测试应结构良好、易于理解，并能适应异步代码的变化。在本次探讨中，我们将深入研究编写清晰且可维护的异步单元测试的最佳实践，包括基于 C# 12 和 .NET 8 异步编程的代码示例和指南。

### 1. 在测试方法中使用 Async/Await：

在测试异步代码时，始终在测试方法中使用 async/await 关键字来干净地处理异步操作。这确保测试方法本身可以等待异步操作，并在整个测试过程中保持异步上下文。

```csharp
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests
{
    [Fact]
    public async Task MyAsyncMethod_ShouldReturnExpectedResult()
    {
        // Arrange
        var myService = new MyService();
    }

    [Fact]
    public async Task MyAsyncMethod_ShouldThrowException()
    {
        // Arrange
        var myService = new MyService();

        // Act & Assert
        await Assert.ThrowsAsync<SomeException>(async () => await myService.MyAsyncMethodThatThrows());
    }
}
```

在第二个测试示例中，使用 `Assert.ThrowsAsync` 来断言异步方法抛出特定异常，从而演示了在测试中正确处理异步异常。

### 3. 使用适当的设置和清理：

在必要时，使用设置和清理方法来设置测试夹具并清理资源。对于异步设置或清理，如果测试框架支持，请使用异步版本（`SetUpAsync`、`TearDownAsync`）。

```csharp
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests : IAsyncLifetime
{
    private MyService _myService;

    public async Task InitializeAsync()
    {
        // Async setup before each test
        _myService = new MyService();

        await Task.CompletedTask;
    }

    [Fact]
    public async Task MyAsyncMethod_ShouldReturnExpectedResult()
    {
        // Act
        int result = await _myService.MyAsyncMethod();

        // Assert
        Assert.Equal(42, result);
    }

    public async Task DisposeAsync()
    {
        // Async teardown after all tests
        await _myService.DisposeAsync();
    }
}
```

### 4. 对异步场景使用参数化测试：

```csharp
public async Task AddAsync_ShouldReturnSum(int a, int b, int expectedSum)
{
    // Arrange
    var calculator = new Calculator();
    // Act
    int result = await calculator.AddAsync(a, b);
    // Assert
    Assert.Equal(expectedSum, result);
}
```

在此示例中，`InlineData` 提供不同的输入值，以测试 `AddAsync` 方法在不同场景下的功能。

### 5. 测试异步错误路径：

确保使用 `Assert.ThrowsAsync` 或类似方法测试异步方法中的异步错误路径和异常处理，以验证正确的异常行为。

```csharp
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests
{
    [Fact]
    public async Task MyAsyncMethod_ShouldThrowException()
    {
        // Arrange
        var myService = new MyService();

        // Act & Assert
```

当使用如 Moq 或 NSubstitute 等框架模拟异步依赖时，请确保使用 `ReturnsAsync` 或等效方法为异步方法或任务设置异步行为。

```csharp
using Moq;
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests
{
    [Fact]
    public async Task ProcessDataAsync_ShouldReturnProcessedValue()
    {
        // Arrange
        var mockDataService = new Mock<IDataService>();
        mockDataService.Setup(d => d.GetDataAsync()).ReturnsAsync(42); // Setup async behavior

        var myService = new MyService(mockDataService.Object);

        // Act
        int result = await myService.ProcessDataAsync();

        // Assert
        Assert.Equal(84, result); // Expected processed value
    }
}
```

在此示例中，我们使用 Moq 模拟 `IDataService` 接口，以模拟 `GetDataAsync` 的异步行为。

### 8. 使用断言方法的异步版本：

一些单元测试框架提供断言方法的异步版本，例如 NUnit 中的 `Assert.EqualAsync` 或 xUnit 中配合 `await` 使用的 `Assert.Equal`，它们对于比较异步结果很有用。

```csharp
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests
{
    [Fact]
    public async Task MyAsyncMethod_ShouldReturnExpectedResult()
    {
        // Arrange
        var myService = new MyService();

        // Act
        int result = await myService.MyAsyncMethod();

        // Assert
        await Assert.EqualAsync(42, result); // Async version of assertion
    }
}
```

### 9. 使用有意义的异步测试命名：

遵循在异步测试方法名称中包含 `Async` 或类似后缀的命名约定，以表明它们是异步的。这使开发人员和工具都清楚地知道该方法是异步测试。

```csharp
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests
{
    [Fact]
    public async Task MyAsyncMethod_ShouldReturnExpectedResult()
    {
        // Arrange
        var myService = new MyService();

        // Act
        int result = await myService.MyAsyncMethod();

        // Assert
        await Assert.EqualAsync(42, result); // Async version of assertion
    }
}
```

### 10. 记录异步测试行为：

在异步测试方法中提供清晰简洁的文档或注释，以描述被测的预期行为、输入和预期结果。这有助于其他开发人员理解测试的目的及其预期。

```csharp
using Xunit;
using System.Threading.Tasks;

public class MyServiceTests
{
    /// <summary>
    /// Verifies that MyAsyncMethod returns the expected result asynchronously.
    /// </summary>
    [Fact]
```


```csharp
public async Task MyAsyncMethod_ShouldReturnExpectedResult()
{
    // Arrange
    var myService = new MyService();

    // Act
    int result = await myService.MyAsyncMethod();

    // Assert
    await Assert.EqualAsync(42, result); // Async version of assertion
}
```

按以下最佳实践，开发人员可以在 C# 12 和 .NET 8 中为其异步代码库创建清晰、可维护且可靠的异步单元测试。利用 async/await 模式、避免阻塞调用、使用适当的设置/拆卸、测试错误路径以及有效组织测试，有助于提高单元测试的质量和可读性。适当模拟异步依赖项、使用断言方法的异步版本以及记录异步测试行为，进一步增强了异步单元测试的清晰度和可维护性。将这些实践纳入整体测试策略，有助于确保异步代码按预期行为，并在一段时间内保持可测试性和可维护性。

# 第 10 章：像专业人士一样调试异步应用程序

### 识别异步代码中的常见陷阱和调试技术

识别常见陷阱并了解异步代码的调试技术对于使用 C# 12 和 .NET 8 的开发人员至关重要。异步编程带来了诸多好处，但也引入了复杂性，可能导致微妙的错误和具有挑战性的调试场景。在本次探讨中，我们将讨论异步代码中的常见陷阱，并提供调试技术以及基于 C# 12 和 .NET 8 异步编程的代码示例。

### 1. 异步代码中的常见陷阱：

- **Async/Await 的不正确使用：** 常见错误是没有正确使用 async/await，例如在异步方法中缺少 `await` 关键字或使用 `Task.Result` 或 `Task.Wait`，这可能导致死锁或阻塞代码。
- **异步代码中的未处理异常：** 如果未使用 try/catch 块正确处理，或未使用 `Task.Exception` 或 `Task.IsFaulted` 属性检查错误，异步代码可能会出现未处理的异常。
- **任务组合不正确：** 在没有适当错误处理的情况下链接多个异步操作，或使用不正确的任务组合方法，如
异步操作、中间状态和潜在错误。使用结构化日志以便更好地分析。
- **审查任务组合：** 审查任务组合和异步模式（例如 async/await、Task.WhenAll、Task.WhenAny），以确保异步工作流中具有适当的错误处理、取消和资源清理。

### 3. 示例调试场景：

让我们考虑一个示例，其中我们有一个错误处理不正确的异步方法，并在执行期间遇到未处理的异常。

```csharp
public async Task<int> DivideAsync(int dividend, int divisor)
{
    try
    {
        await Task.Delay(100); // Simulate async operation
        return dividend / divisor;
    }
    catch (DivideByZeroException)
    {
        // Incorrect error handling
        return -1; // Return a default value
    }
}

public class Program
{
    public static async Task Main(string[] args)
    {
        try
        {
            int result = await DivideAsync(10, 0); // Divide by zero
            Console.WriteLine($"Result: {result}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Exception caught: {ex}");
        }
    }
}
```

在此示例中，`DivideAsync` 方法未正确处理 `DivideByZeroException` 并返回默认值。当在 `Main` 中执行 `DivideAsync(10, 0)` 时，它会遇到除零异常，但异常未在 `DivideAsync` 方法中正确捕获。

### 调试步骤：

1. **启用调试工具：** 确保调试器配置为在 Tasks 中未处理的异常时中断，以便在调试期间捕获异步异常。
2. **查看异步调用堆栈：** 使用异步堆栈跟踪和调试器断点检查导致异常的调用链。
3. **检查异常详情：** 当异常被捕获时，检查异常详情（例如 消息、堆栈跟踪），以了解异常的原因和上下文。
4. **修复错误处理：** 更新 `DivideAsync` 方法以正确处理 `DivideByZeroException`，要么抛出自定义异常，要么返回有意义的错误值。
5. **测试并验证：** 修复错误处理后，再次测试异步方法并验证其按预期行为且没有未处理的异常。

识别常见陷阱并掌握调试技术是使用 C# 12 和 .NET 8 中异步代码的开发人员必备技能。通过意识到诸如不正确的异步使用、未处理的异常、任务组合问题、资源管理以及同步问题等陷阱，开发人员可以编写更健壮可靠的异步代码。利用调试工具、异步堆栈跟踪、日志记录、结构化错误处理和适当的异常管理是诊断和高效解决异步代码中问题的关键技术。将这些实践纳入开发工作流程可提高代码质量、减少错误并增强现代 C# 和 .NET 环境中异步应用程序的整体可靠性。

### 利用调试工具跟踪异步执行流程

利用调试工具跟踪异步执行流程对于理解和诊断使用 C# 12 和 .NET 8 开发的异步代码库中的问题至关重要。异步编程在执行流程中引入了复杂性，如果没有适当的工具，调试会变得具有挑战性。在本次探讨中，我们将讨论 Visual Studio 和其他环境中用于跟踪异步执行流程的各种调试工具和技术，以及基于 C# 12 和 .NET 8 异步编程的代码示例。

1. **异步堆栈跟踪：** 异步堆栈跟踪提供有关异步代码中调用链和 await 点的详细信息，帮助开发人员了解异步操作的流程。Visual Studio 和其他调试工具支持异步堆栈跟踪，使跟踪异步方法调用变得更容易。

```csharp
public async Task<int> DivideAsync(int dividend, int divisor)
{
    await Task.Delay(100); // Simulate async operation
    return dividend / divisor;
}

public class Program
{
    public static async Task Main(string[] args)
    {
        int result = await DivideAsync(10, 2);
        Console.WriteLine($"Result: {result}");
    }
}
```

使用 Visual Studio 调试 `DivideAsync` 方法时，您可以检查调用堆栈并查看指示 await 点和异步方法调用的异步帧。

### 2. Visual Studio 调试工具：

Visual Studio 提供了强大的调试工具用于跟踪异步执行流程。以下是一些可用的功能和技术：

**异步调用堆栈窗口：**

- 在调试异步方法时打开异步调用堆栈窗口（`Debug > Windows > Async Call Stack`），以查看调用堆栈中的异步帧和 await 点。
- 异步调用堆栈窗口显示异步方法的层次结构以及代码当前等待异步操作完成的位置。

**任务列表和状态：**

- 在 Visual Studio 的任务列表窗口（`View > Task List`）中，您可以看到异步执行期间处于等待、已完成或出错状态的任务。
- 这有助于跟踪异步任务的状态并识别潜在问题，例如未处理的异常或卡住的任务。

**异常设置：**

- 配置 Visual Studio 的异常设置（`Debug > Windows > Exception Settings`），以在常见异步异常（如 `System.AggregateException`、`System.Threading.Tasks.TaskCanceledException`）或与您的异步代码相关的特定异常时中断。
- 在异常时中断有助于在异步执行期间捕获和诊断错误。

### 3. 调试异步状态机：

C# 中的异步方法在幕后生成状态机来管理异步操作。Visual Studio 的调试工具允许您逐步执行异步状态机并了解异步代码如何转换为状态机逻辑。

**示例：**

```csharp
public async Task<int> MultiplyAsync(int a, int b)
{
    await Task.Delay(100); // Simulate async operation
    return a * b;
}
public async Task<int> PerformOperationsAsync()
```

{
    int result1 = await MultiplyAsync(10, 2);
    int result2 = await MultiplyAsync(result1, 3);
    return result2;
}

当调试 `PerformOperationsAsync` 时，使用 Visual Studio 的逐步进入（`F11`）来逐步执行异步状态机，并观察 `await` 点如何转换为状态机状态。

## 4. 日志记录与追踪：

日志记录和追踪是理解异步执行流程的有价值技术，尤其是在分布式系统或多线程场景中。为你的异步代码添加日志语句，以跟踪异步方法调用、中间状态、输入/输出值以及潜在错误。

## 示例：

```csharp
public async Task<int> DivideAsync(int dividend, int divisor)
{
    try
    {
        await Task.Delay(100); // Simulate async operation
        int result = dividend / divisor;
        Console.WriteLine($"DivideAsync: {dividend} / {divisor} = {result}");
        return result;
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine($"DivideAsync Error: {ex.Message}");
        throw;
    }
}
```

```csharp
public class Program
{
    public static async Task Main(string[] args)
    {
        try
        {
            int result = await DivideAsync(10, 0); // Divide by zero
            Console.WriteLine($"Result: {result}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Exception caught: {ex}");
        }
    }
}
```

在此示例中，向 `DivideAsync` 添加了日志语句以记录输入值和错误，从而提供对异步执行流程的洞察。

## 5. 异步调试最佳实践：

-  strategically 使用断点在异步方法中的关键点暂停执行并观察异步状态。
- 使用逐步进入（`F11`）和逐步跳过（`F10`）逐步执行异步代码，以了解异步操作如何进展。
- 在 Visual Studio 中启用调试优化（`Debug > Options > Debugging > General`）以获得更顺畅的调试体验，尤其是在复杂的异步场景中。
- 在异步调试期间利用条件断点和数据提示来检查变量和表达式。

使用调试工具追踪异步执行流程对于理解、诊断和解决使用 C# 12 和 .NET 8 开发的异步代码库中的问题至关重要。Visual Studio 的异步调试功能，如异步调用堆栈、异步调用堆栈窗口、任务列表和异常设置，为异步方法调用、await 点、任务状态和异步状态机提供了宝贵的洞察。将调试工具与日志记录、追踪以及异步调试的最佳实践相结合，增强了开发人员有效识别和调试与异步相关问题的能力，从而带来更可靠、可维护的异步代码库。将这些技术纳入你的异步调试工作流程，以简化故障排除并提高异步编程场景中的整体开发生产力。

## 在异步代码中有效处理异常和错误场景

在异步代码中有效处理异常和错误场景对于使用 C# 12 和 .NET 8 开发健壮可靠的应用程序至关重要。异步编程引入了复杂性，错误可能在异步操作期间发生。在此探索中，我们将讨论处理异步代码中异常和错误场景的最佳实践、模式和代码示例。

## 1. 异常处理基础：

异步代码中的异常处理遵循与同步代码相同的原则，但需要关注任务、异步方法和 await 表达式等异步特定构造。关键点包括：

- **尝试/捕获块：** 使用 try/catch 块在异步方法内捕获异常并适当地处理它们。
- **AggregateException：** 当使用 `Task.WhenAll` 或类似方法并发等待多个任务时，各个任务的异常会被聚合到一个 `AggregateException` 中。

## 2. 在异步方法中正确处理异常：

设计异步方法时，考虑异常应如何处理并传播给调用方。以下是一些最佳实践：

- **传播异常：** 除非你能在异步方法内部处理并从异常中恢复，否则考虑将异常传播给调用方。

```csharp
public async Task<int> DivideAsync(int dividend, int divisor)
{
    await Task.Delay(100); // Simulate async operation
    if (divisor == 0)
    {
        throw new ArgumentException("Divisor cannot be zero.");
    }
    return dividend / divisor;
}
```

为避免未观察到的任务异常并确保所有任务都被观察到。

- **`Task.WhenAll` 异常处理：**
  当使用 `Task.WhenAll` 并发等待多个任务时，使用 `Task.WhenAll` 结合 `Task.WhenAny` 处理异常。

```csharp
public async Task<int[]> ProcessDataAsync()
{
    Task<int> task1 = GetDataAsync(1);
    Task<int> task2 = GetDataAsync(2);

    var tasks = new[] { task1, task2 };

    Task<int[]> allTasks = Task.WhenAll(tasks);

    try
    {
        await allTasks;
        return allTasks.Result; // Access results after await
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Exception occurred: {ex.Message}");
        // Handle or log the exception
        return null; // Return null or default value
    }
}

public async Task<int> GetDataAsync(int value)
{
    await Task.Delay(100); // Simulate async operation
    if (value == 0)
    {
        throw new ArgumentException("Value cannot be zero.");
    }
    return value * 10;
}
```

在此示例中，`ProcessDataAsync` 等待 `Task.WhenAll` 以并发处理多个异步操作并适当地处理异常。

- `Task.WhenAny` 超时：使用 `Task.WhenAny` 配合超时来处理异步操作耗时超过预期时的场景。

```csharp
public async Task<int>
PerformOperationWithTimeoutAsync()
{
    Task<int> operationTask =
        SomeLongRunningOperationAsync();
    Task delayTask = Task.Delay(TimeSpan.FromSeconds(5));
    // Timeout

    Task completedTask = await
        Task.WhenAny(operationTask, delayTask);

    if (completedTask == delayTask)
    {
        throw new TimeoutException("Operation timed out.");
    }

    return await operationTask; // Await the completed
    operation
}
```

在此示例中，`PerformOperationWithTimeoutAsync` 使用 `Task.WhenAny` 来处理长时间运行操作期间的超时场景。

## 4. 使用 `try/catch` 与 `await`：

当等待可能抛出异常的任务时，使用 `try/catch` 块围绕 `await` 语句以处理该 await 点特定的异常。

```csharp
public async Task<int> DivideAsync(int dividend, int divisor)
{
    try
    {
        await Task.Delay(100); // Simulate async operation
        return dividend / divisor;
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine($"Divide by zero error: {ex.Message}");
        throw; // Re-throw the exception to propagate it
    }
}
```

## 5. 日志记录与错误报告：

除在异步方法内部处理异常外，日志记录和错误报告在识别和诊断异步代码中的问题方面发挥着至关重要的作用。

## 示例：

```csharp
public async Task<int> ProcessDataAsync(int id)
{
    try
    {
        var data = await GetDataAsync(id);
        // Process data
        return data.Length;
    }
    catch (Exception ex)
    {
        Logger.LogError($"Error processing data: {ex.Message}");
        throw; // Re-throw the exception for higher-level handling
    }
}
```

在此示例中，`Logger.LogError` 记录错误消息，使开发人员或管理员能够查看日志并诊断问题。

## 6. 处理聚合异常：

当使用 `Task.WhenAll` 并发等待多个任务时，处理 `AggregateException` 以检查各个任务的异常。

```csharp
public async Task ProcessMultipleTasksAsync()
{
    Task task1 = Task.Run(() => { throw new InvalidOperationException("Task 1 error"); });
    Task task2 = Task.Run(() => { throw new ArgumentException("Task 2 error"); });

    try
    {
        await Task.WhenAll(task1, task2);
    }
    catch (AggregateException ex)
```

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

# 第 11 章：设计结构良好的异步 API 和模式

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

```csharp
    _queue.Enqueue(data);
}
}
private int DequeueData()
{
    lock (_lock)
    {
        return _queue.Count > 0 ? _queue.Dequeue() : -1;
    }
}

private void ProcessData(int data)
{
    Console.WriteLine($"Consumed data: {data}");
}
```

在此示例中，`StartProducer` 和 `StartConsumer` 方法分别模拟生产者和消费者的角色。生产者异步生成数据并将其加入共享队列，而消费者则异步出队并处理数据。

## 2. 事件驱动模式：
事件驱动模式是另一种强大的异步设计模式，它依赖事件和事件处理程序来处理异步操作。它通常用于用户界面、异步通信和解耦系统。

## 关键组件：
- **事件：** 表示触发事件处理程序的发生事件或操作。

```csharp
}
    private async void EventDriven_DataReceived(object sender, DataEventArgs e)
    {
        await Task.Delay(1000); // Simulate processing delay
        Console.WriteLine($"Data Received: {e.Data}");
    }
}
```

在此示例中，`EventDrivenExample` 异步模拟数据传输，并在收到数据时触发 `DataReceived` 事件。`EventSubscriber` 订阅此事件并异步处理接收到的数据。

## 使用异步设计模式的好处：
## 1. 清晰性与关注点分离：
- 生产者-消费者和事件驱动等设计模式促进了数据生成/消费与处理逻辑之间的清晰分离。
- 它们通过将异步操作组织到不同的组件中，增强了代码的可读性和可维护性。

**2. 并发性与可扩展性：** 异步模式促进了并行和并发，允许多个任务在不阻塞的情况下并发执行。

**3. 异步协调：** 生产者-消费者等模式有效处理异步协调和同步，确保共享资源的安全访问。

4. **解耦与灵活性：** 事件驱动模式解耦了组件，促进了灵活且可扩展的松耦合架构。

## 异步设计模式的最佳实践：
- **使用 Async/Await：** 使用 `async` 和 `await` 关键字实现异步操作，以利用非阻塞 I/O 和并发。
- **线程安全：** 使用同步机制（如锁（`lock` 关键字）、并发集合或同步原语）确保共享资源的线程安全。
- **错误处理：** 在异步组件中适当处理异常，并将错误传播到更高层进行集中式错误处理。
- **文档：** 为事件、事件处理程序和异步方法提供清晰的文档，以指导使用者和开发者。

在 C# 12 和 .NET 8 中，利用常见的异步设计模式（如生产者-消费者模式和事件驱动模式）有助于创建结构良好、高效且可扩展的异步 API 和系统。这些模式促进了清晰性、关注点分离、并发性和灵活性，从而带来可维护且响应迅速的应用程序。通过理解异步设计模式的原则、组件和最佳实践，开发者可以利用异步编程的强大功能来处理复杂的异步工作流，并提高应用程序的整体性能和可靠性。在异步编程项目中有意识地融入这些模式，以实现更简洁、更可维护、更高效的异步代码库。

## 在异步代码中确保线程安全并避免竞态条件
在异步编程中，确保线程安全并避免竞态条件对于维护数据完整性和防止意外行为至关重要。在 C# 12 和 .NET 8 中，异步编程引入了并发性，多个线程可以同时访问共享资源。如果处理不当，这种并发性可能导致竞态条件和数据损坏。在本次探讨中，我们将讨论在异步代码中确保线程安全并避免竞态条件的策略、技术和代码示例。

## 理解线程安全与竞态条件：
## 1. 线程安全：
- 线程安全是指当多个线程并发访问共享资源时，代码能够正确运行的能力。
- 确保线程安全涉及同步对共享数据的访问，以防止数据损坏、竞态条件和不一致。

## 2. 竞态条件：
- 当程序的结果取决于线程执行的时序或顺序时，就会发生竞态条件。
- 并发线程在没有适当同步的情况下访问和修改共享数据，可能导致竞态条件和错误结果。

## 确保线程安全的技术：
## 1. 锁定机制：
- 使用 `lock` 语句或 `Mutex` 等锁定机制来同步对共享资源的访问。
- `lock` 语句确保每次只有一个线程可以进入代码的关键部分，从而防止并发访问。

## 2. 线程安全集合：
- 利用 .NET 提供的线程安全集合（如 `ConcurrentQueue`、`ConcurrentDictionary` 和 `ConcurrentBag`）进行共享数据访问。
- 这些集合旨在无需显式锁定即可安全处理并发访问。

## 3. 不可变数据结构：
- 尽可能使用不可变数据结构，以避免锁定需求。
- 不可变对象在创建后无法修改，因此对于只读操作本质上就是线程安全的。

## 使用锁定机制的示例：
```csharp
public class Counter
{
    private int _count;
    private readonly object _lockObject = new object();

    public int IncrementAndGet()
    {
        lock (_lockObject)
        {
            _count++;
            return _count;
        }
    }
}
```

在此示例中，`Counter` 类的 `IncrementAndGet` 方法使用 `lock` 语句来确保递增 `_count` 字段时的线程安全。

## 避免死锁：
## 1. 避免嵌套锁：
- 避免嵌套锁，因为这可能导致死锁，即线程互相无限期等待。
- 如果必须获取多个锁，请确保在所有代码路径中以一致的顺序获取它们。

## 2. 超时与 Try/Catch：
- 在获取锁时使用超时和 try/catch 块，以优雅地处理潜在的死锁场景。
- 考虑使用 `Monitor.TryEnter` 或带超时的 `Monitor.Enter`，以更好地控制锁的获取。

## 使用 Try/Catch 和超时的示例：
```csharp
public class Account
{
    private decimal _balance;
    private readonly object _lockObject = new object();

    public void Withdraw(decimal amount)
    {
        bool lockAcquired = false;
        try
        {
            lockAcquired = Monitor.TryEnter(_lockObject, TimeSpan.FromSeconds(1)); // Acquire lock with timeout
            if (lockAcquired)
            {
                if (_balance >= amount)
                {
                    _balance -= amount;
                    Console.WriteLine($"Withdrawn: ${amount}, Remaining Balance: ${_balance}");
                }
                else
                {
                    Console.WriteLine("Insufficient balance.");
                }
            }
            else
            {
                Console.WriteLine("Failed to acquire lock within timeout.");
            }
        }
        finally
        {
            if (lockAcquired)
            {
                Monitor.Exit(_lockObject); // Release the lock
            }
        }
    }
}
```

## 异步代码与线程安全：
## 1. Async/Await 与锁：
- 使用 async/await 时，锁仍然可以有效确保线程安全。
- 确保异步方法的关键部分受锁保护，以避免并发访问问题。

## 2. 线程安全异步集合：
对于涉及共享数据的异步代码，使用像 `ConcurrentQueue<T>` 或 `ConcurrentDictionary<TKey, TValue>` 这样的线程安全异步集合。

## 使用异步锁定的示例：
```csharp
public class AsyncCounter
{
    private int _count;
    private readonly AsyncLock _asyncLock = new AsyncLock();

    public async Task<int> IncrementAndGetAsync()
    {
        using (await _asyncLock.LockAsync())
        {
            _count++;
            return _count;
        }
    }
}
```

在此示例中，`AsyncCounter` 使用 `AsyncLock`（`lock` 的异步版本）来确保像 `IncrementAndGetAsync` 这样的异步方法中的线程安全。




在 C# 12 和 .NET 8 中，确保异步代码的线程安全并避免竞态条件，对于构建可靠且可扩展的应用程序至关重要。通过理解线程安全概念、利用锁定机制、线程安全集合、不可变数据结构，并处理潜在的死锁，开发人员可以编写在多线程环境中正确执行并保持数据完整性的并发代码。在使用异步编程时，请记住在整个代码库中一致地应用线程安全技术，尤其是在并发访问或修改共享资源的场景中。以下是额外的最佳实践，作为关于确保异步代码线程安全和避免竞态条件讨论的总结：

## 附加最佳实践：

- **1. 原子操作：** 将涉及多个步骤但必须原子执行的操作封装在锁内，或使用 `Interlocked` 类等原子构造，对数值类型执行线程安全操作。

```csharp
private int _counter;

public void IncrementCounter()
{
    Interlocked.Increment(ref _counter);
}
```

- **2. 避免共享可变状态：** 尽可能使用不可变对象或将可变状态隔离在特定作用域内，以减少共享可变状态，从而降低竞态条件的可能性。

- **3. UI 应用程序中的同步上下文：** 在 WPF 或 WinForms 等 UI 应用程序中，确保使用 `Dispatcher`（WPF）或 `Control.Invoke`（WinForms）等同步机制从 UI 线程访问 UI 相关代码，以避免跨线程问题。

- **4. 线程安全测试：**
  - 编写全面的单元测试，模拟对共享资源的并发访问，以验证线程安全性。
  - 使用并发测试工具或库（如 `Microsoft.VisualStudio.Threading.Analyzers`）检测代码中潜在的线程安全问题。

- **5. 异步锁定：** 对于异步方法，请考虑使用异步锁定机制（如示例中的 `AsyncLock`）或 `SemaphoreSlim`，在异步代码中实现非阻塞同步。

### 使用 SemaphoreSlim 的示例：

```csharp
public class AsyncResource
{
    private readonly SemaphoreSlim _semaphore = new SemaphoreSlim(1, 1); // Allow one concurrent access

    public async Task AccessResourceAsync()
    {
        await _semaphore.WaitAsync(); // Acquire the semaphore
        try
        {
            // Access shared resource asynchronously
        }
        finally
        {
            _semaphore.Release(); // Release the semaphore
        }
    }
}
```

确保线程安全和避免竞态条件是编写健壮且可扩展的 C# 12 和 .NET 8 异步代码的基本方面。通过应用线程安全技术，如使用锁定机制、原子操作、避免共享可变状态以及进行线程安全测试，开发人员可以创建有效处理共享资源并发访问的应用程序，并防止因竞态条件导致的数据损坏或意外行为。理解并发和同步的原理对于在异步编程环境中构建高性能且可靠的软件系统至关重要。将这些最佳实践融入你的开发工作流程，以确保代码库的线程安全性和弹性，满足现代多线程应用程序的需求。

# 第 12 章

### 使用性能分析工具识别异步代码中的性能瓶颈

识别异步代码中的性能瓶颈对于优化使用 C# 12 和 .NET 8 开发的应用程序的效率和响应能力至关重要。异步编程可以提高并发性和可扩展性，但如果管理不当，也会引入可能导致性能问题的复杂性。在本次探讨中，我们将讨论识别和诊断异步代码性能瓶颈的技术和工具，以及代码示例和最佳实践。

### 理解异步代码中的性能瓶颈：

- **1. CPU 密集型与 I/O 密集型操作：**
  - CPU 密集型操作会大量消耗处理器资源，而 I/O 密集型操作则涉及等待外部资源，如磁盘 I/O、网络调用或数据库查询。
  - 识别操作是 CPU 密集型还是 I/O 密集型，有助于选择适当的异步模式和优化方案。

- **2. 争用与同步：**
  - 当多个线程竞争共享资源时会出现争用，导致锁争用和并行度降低。
  - 同步开销（如锁或同步原语）会影响性能，尤其是在高并发场景中。

- **3. 异步开销：**
  - 异步编程会因上下文切换、任务调度和延续管理而产生开销。
  - 高效使用异步模式并避免不必要的 async/await 调用可以减轻这种开销。

### 性能分析工具：

- **1. Visual Studio 分析器：**
  - Visual Studio 提供了用于 .NET 应用程序性能分析的内置分析工具，包括 CPU 分析、内存分析和性能诊断。
  - 使用 Visual Studio 中的性能分析器来识别热路径、CPU 使用率、内存分配和异步调用堆栈。

- **2. JetBrains 的 DotTrace：**
  - DotTrace 是一款强大的性能分析工具，支持 .NET 应用程序，并提供有关 CPU 使用率、线程活动、异步调用和内存使用情况的详细见解。
  - 使用 DotTrace 分析异步调用链、识别阻塞操作，并精确定位异步代码中的性能瓶颈。

- **3. AsyncProfiler：**
  - AsyncProfiler 是一款专门用于分析异步应用程序并识别与异步操作、任务调度和线程同步相关的瓶颈的工具。
  - 它可以分析 async/await 模式、await 延续、线程池使用情况以及异步代码特有的并发问题。

### 识别性能瓶颈的技巧：

- **1. CPU 分析：**
  - 使用 CPU 分析工具识别消耗大量 CPU 时间的方法或代码段。
  - 分析异步操作期间的 CPU 使用率，以检测 CPU 密集型瓶颈。

- **2. 内存分析：**
  - 内存分析有助于识别异步代码中的内存泄漏、过度分配和低效的内存使用模式。
  - 分析异步操作期间的内存分配和释放模式，以优化内存使用。

- **3. 异步调用堆栈：**
  - 分析异步调用堆栈，以了解异步操作的流程、await 延续和任务调度行为。
  - 识别可能导致延迟并影响整体性能的阻塞或长时间运行的异步方法。

### 使用 Visual Studio 进行性能分析的示例：

- **1. 在异步方法中明智地使用 `Task.Run` 处理 CPU 密集型操作。**

- **2. 避免阻塞调用：**
  - 尽量减少或避免异步方法中的阻塞调用（`Task.Result`、`Thread.Sleep`），因为它们会降低性能并导致线程争用。

- **3. 优化同步：**
  - 审查并优化同步机制（锁、信号量）以减少争用并提高并行度。
  - 在高吞吐量场景中，考虑使用无锁算法或并发数据结构。

- **4. 批处理与并行化：**
  - 尽可能批量处理 I/O 操作并并行化 CPU 密集型任务，以充分利用多核处理器并提高吞吐量。
  - 使用 `Parallel.ForEach` 或 PLINQ 等并行构造进行 CPU 密集型并行处理。

- **5. 监控与分析：**
  - 使用性能分析工具和性能计数器持续监控应用程序性能，以识别趋势、异常和潜在瓶颈。
  - 在开发和生产环境中分析性能指标，以确保不同场景下的最佳性能。

识别异步代码中的性能瓶颈需要结合性能分析工具、最佳实践和优化技术。通过利用像 Visual 这样的工具

使用 Studio Profiler、DotTrace 或专业的异步分析器，开发人员可以深入了解 CPU 使用率、内存分配、异步调用堆栈和同步模式。分析异步操作的 CPU 密集型和 I/O 密集型方面、优化同步机制、避免阻塞调用并监控性能指标对于实现高效且可扩展的异步代码至关重要。将性能分析纳入开发生命周期，以持续改进异步应用程序的性能并提供响应迅速的用户体验。

## 应用优化技术以提高效率（例如，任务取消、内存管理）

应用优化技术对于提高 C# 12 和 .NET 8 中异步代码的效率、响应性和资源利用率至关重要。优化技术专注于任务取消、内存管理、资源池化和性能调优等领域，以提升异步应用程序的整体性能。在本次探讨中，我们将通过代码示例和最佳实践深入了解这些优化技术。

### 任务取消

任务取消对于管理异步操作和确保应用程序的响应行为至关重要，尤其是在需要根据用户输入或系统条件取消或中止长时间运行任务的场景中。

**使用 CancellationToken:**

```csharp
public class TaskCancellationExample
{
    public async Task ProcessDataAsync(CancellationToken cancellationToken)
    {
        try
        {
            await Task.Delay(5000, cancellationToken); // Simulate long-running operation
            Console.WriteLine("Task completed.");
        }
        catch (TaskCanceledException)
        {
            Console.WriteLine("Task was canceled.");
        }
    }
}
```

在上面的示例中，`ProcessDataAsync` 方法接受一个 `CancellationToken` 以允许取消异步操作。在方法内部使用 `cancellationToken.ThrowIfCancellationRequested()` 来检查取消。

### 最佳实践

- **传递 CancellationToken：** 始终将 `CancellationToken` 传递给异步方法，并在调用链中传播取消。
- **处理取消：** 使用 try-catch 块捕获 `TaskCanceledException`，或在异步方法内检查 `cancellationToken.IsCancellationRequested`。
- **取消挂起的任务：** 在请求取消时及时取消挂起的任务，以释放缓冲区并避免不必要的堆分配。
- **释放资源：** 始终正确释放资源（如内存池、流），以便及时释放资源并避免内存泄漏。
- **避免大对象堆（LOH）：** 最小化大对象的分配，以防止 LOH 碎片化并提高垃圾回收性能。

### 异步性能调优

优化异步性能涉及调整并发级别、并行性、异步模式和资源利用率等各个方面，以实现最佳吞吐量和响应性。

**使用并行性:**

```csharp
public class ParallelismExample
{
    public async Task<int> ProcessDataAsync()
    {
        var tasks = new List<Task<int>>();
        for (int i = 0; i < 10; i++)
        {
            tasks.Add(ProcessDataItemAsync(i));
        }
        await Task.WhenAll(tasks); // Wait for all tasks to complete
        return tasks.Sum(t => t.Result);
    }

    private async Task<int> ProcessDataItemAsync(int item)
    {
        await Task.Delay(100); // Simulate processing delay
        return item * 2;
    }
}
```

在此示例中，`ProcessDataAsync` 使用并行任务并发处理多个数据项，以利用 CPU 核心并提高整体处理速度。

### 最佳实践

- **并行化独立任务：** 识别并并行化独立任务，以利用多核处理器并提高并发性。
- **避免阻塞调用：** 在异步方法中尽量减少或消除阻塞调用（`Task.Result`、`Thread.Sleep`），以保持响应性。
- **优化 Await 链：** 避免深度嵌套的 await 链，并考虑重构异步操作以获得更好的可读性和性能。

### 资源池化

资源池化技术有助于高效地管理和重用数据库连接、HTTP 连接和线程池等资源，减少开销并提高可扩展性。

**使用连接池:**

```csharp
public class ConnectionPoolingExample
{
    private readonly IDbConnectionFactory _dbConnectionFactory;

    public ConnectionPoolingExample(IDbConnectionFactory dbConnectionFactory)
    {
        _dbConnectionFactory = dbConnectionFactory;
    }

    public async Task<string> ExecuteQueryAsync()
    {
        using (var connection = _dbConnectionFactory.GetConnection())
        {
            // Execute database query using connection
            await Task.Delay(100); // Simulate database operation
            return "Query Result";
        }
    }
}
```

在此示例中，`IDbConnectionFactory` 抽象了数据库连接的创建，允许连接池化并在异步操作中高效重用数据库连接。

### 最佳实践

- **使用连接池：** 对于数据库连接、HTTP 连接和其他资源密集型操作，利用连接池以最小化连接开销。
- **正确释放资源：** 使用后始终正确释放资源，以便将池化资源归还到池中供重用。
- **调整池大小：** 根据应用程序工作负载和资源可用性配置最佳池大小，以平衡资源利用率和性能。

应用诸如任务取消、内存管理、异步性能调优和资源池化等优化技术，对于提高 C# 12 和 .NET 8 应用程序中异步代码的效率、响应性和可扩展性至关重要。通过采用最佳实践、有效利用异步模式并优化资源利用，开发人员可以提升应用程序的整体性能并提供流畅且响应迅速的用户体验。持续监控性能指标、分析应用程序行为并迭代优化策略，以在异步编程场景中实现最佳性能。将这些优化技术纳入开发工作流程，以构建满足现代软件开发需求的高性能且高效的异步应用程序。

## 平衡并发与资源利用以实现最佳性能

平衡并发与资源利用对于使用 C# 12 和 .NET 8 进行异步编程时实现最佳性能至关重要。异步编程允许任务并发执行，但在优化资源使用的同时有效管理并发需要仔细考虑任务调度、线程管理和资源池化等因素。在本次探讨中，我们将深入研究平衡并发与资源利用以实现异步应用程序最佳性能的技术、模式和最佳实践，并附带代码示例。

### 了解并发与资源利用

- **1. 并发管理：**
  - 并发使多个任务能够同时运行，从而提高吞吐量和响应性。
  - 管理并发涉及任务调度、同步以及系统资源的高效使用。
- **2. 资源利用：**
  - 资源利用是指 CPU、内存、I/O 资源和外部服务等的高效使用。
  - 优化资源使用可最大限度减少瓶颈、降低开销并增强应用程序性能。

### C# 12 中的基于任务的并发

C# 12 提供了强大的异步编程构造，包括任务、async/await 和并行功能，可用于有效平衡并发与资源利用。

**基于任务的并发示例:**

```csharp
public class ConcurrencyExample
{
    public async Task<int> ProcessDataAsync()
    {
        var tasks = new List<Task<int>>();
        for (int i = 0; i < 10; i++)
        {
            tasks.Add(ProcessDataItemAsync(i));
        }
        await Task.WhenAll(tasks); // Wait for all tasks to complete
        return tasks.Sum(t => t.Result);
    }
}
```


```csharp
    }
    private async Task<int> ProcessDataItemAsync(int item)
    {
        await Task.Delay(100); // Simulate processing delay
        return item * 2;
    }
}
```

在此示例中，`ProcessDataAsync` 使用任务并发处理多个数据项，借助并行性高效利用 CPU 核心。

## 平衡并发与资源利用的技术：

- 1. **线程池与任务计划程序：**
  - 利用线程池和任务计划程序高效地管理任务执行与线程分配。
  - 根据工作负载特征调整线程池设置（例如 minThreads、maxThreads），以实现最佳并发。
- 2. **Async/Await 模式：**
  - 审慎使用 async/await 模式，避免阻塞调用，并在异步操作期间最大化资源利用率。
  - 对于 I/O 密集型操作可考虑使用 async/await；对于异步方法中的 CPU 密集型操作可考虑使用 Task.Run。
- 3. **任务并行库（TPL）：**
  - 利用 TPL 构造（如 Parallel.ForEach、Parallel.Invoke 和 PLINQ）实现数据并行与集合的并发处理。
  - 根据硬件能力、工作负载特征和可扩展性要求来平衡并行度。
- 4. **资源池化与复用：**
  - 实施资源池化技术（例如连接池、内存池），高效复用资源并最大限度地减少开销。
  - 对数据库连接、HTTP 连接和其他资源进行池化，可降低资源创建与销毁的成本。

### 资源池化示例：

```csharp
public class ResourcePoolingExample
{
    private readonly IDbConnectionFactory _dbConnectionFactory;

    public ResourcePoolingExample(IDbConnectionFactory dbConnectionFactory)
    {
        _dbConnectionFactory = dbConnectionFactory;
    }

    public async Task<string> ExecuteQueryAsync()
    {
        using (var connection = _dbConnectionFactory.GetConnection())
        {
            // Execute database query using pooled connection
            await Task.Delay(100); // Simulate database operation
            return "Query Result";
        }
    }
}
```

此处，`IDbConnectionFactory` 对数据库连接的创建进行了带池化的抽象，从而优化资源使用并降低连接开销。

## 优化并发与资源利用的最佳实践：

- 1. **微调并发度：** 根据工作负载特征、硬件能力和系统资源调整并发级别，以避免资源利用不足或过载。
- 2. **使用异步 I/O 操作：** 优先采用异步 I/O 操作（例如异步数据库调用、异步文件 I/O），以在不阻塞线程的情况下最大化 CPU 利用率和响应速度。
- 3. **批处理与分块：** 对数据处理操作进行批处理和分块，以优化资源利用率，并减少并行与并发场景中的开销。
- 4. **监控与调优性能：** 监控应用性能指标（CPU 使用率、内存使用率、线程利用率），并根据性能剖析和分析结果微调并发设置与资源管理策略。

平衡并发与资源利用是使用 C# 12 和 .NET 8 进行异步编程时优化性能的关键方面。通过利用基于任务的并发、async/await 模式、TPL 构造、资源池化及优化技术，开发者可以在应用中实现最佳的性能、可扩展性和响应速度。理解工作负载特征、系统资源和并发模型，对于在并发执行、高效资源利用和响应速度之间取得平衡至关重要。持续监控性能指标、剖析应用行为，并迭代优化策略，从而为高性能异步应用实现最佳的并发与资源利用。将这些最佳实践和技术融入异步编程工作流，有助于构建高效、可扩展且响应迅速的应用，满足现代软件开发的需求。

# 结论

使用 C# 12 和 .NET 8 进行异步编程，彻底改变了开发者设计和实现高性能、可扩展、响应迅速的应用的方式。借助任务、async/await 和任务并行库（TPL）等异步编程构造，开发者可以充分发挥现代硬件架构的全部潜力，优化资源利用，并提供卓越的用户体验。让我们基于 C# 12 与 .NET 8 的异步编程之旅，深入探讨一个引人入胜的结论。

### 异步编程的力量：

异步编程已成为现代软件开发的基石，使应用能够高效处理并发操作，同时保持响应速度。通过利用异步模式，开发者可以将复杂任务拆分为更小、并发运行的异步操作，减少阻塞和等待时间，从而提升整体系统性能。

### 可扩展性与响应速度：

异步编程的关键优势之一，在于它能够让应用扩展以处理大量并发操作。无论是处理 Web 服务器中的多个请求、执行 I/O 密集型操作，还是运行 CPU 密集型任务，异步编程都支持应用进行水平与垂直扩展，利用多核处理器和异步 I/O 操作实现最佳性能。

### 优化资源利用：

优化资源利用对于在现代应用中实现最佳性能至关重要。借助任务取消、内存管理、资源池化和并发管理技术，开发者可以在高效资源利用与高并发之间取得平衡。通过有效管理线程、任务和资源，应用可以最小化开销、减少争用，并最大化利用可用的系统资源。

### 平衡并发与效率：

异步编程的一大关键挑战是平衡并发与效率。这涉及微调并行度、优化 async/await 模式、批处理操作以及审慎使用异步构造。通过平衡并发与效率，开发者可以实现最佳的吞吐量、响应速度和资源利用率，从而打造高性能、可扩展的应用。

### 持续改进与最佳实践：

异步编程不仅仅是编写代码，更是一种思维方式，以及一套随应用需求和性能要求不断演进的最佳实践。持续监控、剖析和性能调优是维持并改进异步应用性能的关键方面。采用最佳实践、利用剖析工具，并紧跟异步编程技术的进步，可确保应用长期保持高效、可靠与快速响应。

### 异步编程的未来：

展望未来，异步编程将继续在构建下一代应用方面发挥关键作用。随着硬件、软件和云技术的不断进步，开发者将探索异步编程的新范式，例如响应式编程、事件驱动架构和无服务器计算。C# 与 .NET 框架的演进将进一步赋能开发者，创造出在性能、可扩展性和用户体验方面表现卓越的异步应用。

总而言之，使用 C# 12 和 .NET 8 进行异步编程，使开发者能够构建满足现代计算环境需求的高性能、可扩展且响应迅速的应用。通过掌握异步编程构造、优化资源利用、平衡并发与效率并采用最佳实践，开发者可以充分释放异步编程的潜力，交付卓越的软件解决方案。当我们拥抱软件开发的未来时，异步编程仍是创新的基石，使我们能够创造出不断突破性能与用户体验边界的软件。





# 附录

### 异步编程术语表

理解 C# 12 和 .NET 8 中异步编程所使用的术语，对于开发者高效地设计、实现和调试异步代码至关重要。以下是与 C# 12 和 .NET 8 中异步编程相关的关键术语和概念的术语表：

### 异步编程词汇表

- **1. 异步编程（Asynchronous Programming）：** 异步编程是一种编程范式，允许任务独立且并发地执行，而不会阻塞主执行线程。
- **2. 任务（Task）：** `Task` 表示一个异步操作，该操作可以被启动、等待并以异步方式管理。它封装了可能异步完成的方法或操作的执行。
- **3. 异步/等待（Async/Await）：** `async` 和 `await` 是 C# 中支持异步编程的关键字。`async` 将方法标记为异步，`await` 用于异步等待任务的完成。
- **4. 基于任务的异步模式（TAP）：** TAP 是 .NET 中异步编程的一种设计模式，强调使用 `Task` 和 `Task<T>` 类型来表示异步操作。
- **5. 并发（Concurrency）：** 并发是指系统同时处理多个任务或操作的能力。异步编程通过允许任务并发运行而不阻塞，从而促进并发。
- **6. I/O 密集型与 CPU 密集型（I/O-Bound vs. CPU-Bound）：** I/O 密集型操作涉及等待输入/输出操作完成，如磁盘 I/O、网络请求或数据库查询。而 CPU 密集型操作则是大量消耗 CPU 资源的计算任务。
- **7. 线程池（ThreadPool）：** 线程池是 .NET 提供的托管线程池，它管理一组工作线程，以高效执行异步和并行任务。
- **8. 任务计划程序（Task Scheduler）：** 任务计划程序负责调度和管理 .NET 中任务的执行。它确保任务在适当的线程上执行，并提供任务优先级机制。
- **9. 延续（Continuation）：** 延续是计划在任务或异步操作完成后运行的操作。延续通常与 async/await 一起使用，以指定后续操作。
- **10. 取消令牌（Cancellation Token）：** `CancellationToken` 是一种用于取消异步操作的机制。它通过向异步操作发出应被取消的信号来实现协作式取消。
- **11. 异步方法（Async Method）：** 异步方法是使用 `async` 关键字标记的方法，表示该方法包含异步操作。异步方法可以使用 `await` 来异步等待其他异步操作完成。
- **12. 可等待类型（Awaitable Types）：** 可等待类型是可与 `await` 关键字一起使用的类型。这包括任务（`Task`）、值任务（`ValueTask`）、实现 `GetAwaiter` 模式的自定义可等待类型，以及异步可枚举类型（`IAsyncEnumerable`）。
- **13. 并行（Parallelism）：** 并行是指多个任务或操作同时执行，通常是在多个 CPU 核心上执行。.NET 中的 TPL（任务并行库）通过 `Parallel.ForEach` 和 PLINQ 等构造促进并行。
- **14. 内存管理（Memory Management）：** 异步编程中的内存管理涉及内存资源的高效分配和释放。内存池化、使用 `Memory<T>` 或 `ArrayPool<T>` 以及管理大型对象堆（LOH）分配等技术对于优化内存使用至关重要。
- **15. 资源池化（Resource Pooling）：** 资源池化涉及重用和管理池化资源，如数据库连接、HTTP 连接和内存缓冲区，以减少开销并提高可扩展性。
- **16. 取消与超时（Cancellation and Timeout）：** 取消机制允许使用取消令牌取消长时间运行的异步操作。超时机制可用于为操作指定最大持续时间，超过该时限后即视为超时。
- **17. 错误处理（Error Handling）：** 异步编程中的错误处理涉及处理异步操作期间可能发生的异常和错误。诸如 `try-catch` 块、`Task` 返回值以及 `Task.Exception` 属性等技术可用于错误处理。

理解这些术语和概念对于掌握 C# 12 和 .NET 8 中的异步编程至关重要，使开发者能够构建高性能、可扩展且响应迅速的应用程序，充分利用异步编程范式的强大能力。

