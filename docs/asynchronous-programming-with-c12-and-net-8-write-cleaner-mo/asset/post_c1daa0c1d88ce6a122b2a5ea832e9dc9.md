
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

In this example, `Task.WhenAll` is used to execute `Task1`, `Task2`, and `Task3` concurrently, and then await their completion. This approach maximizes CPU utilization by allowing tasks to run in parallel.

## 2. Limiting Concurrent Tasks with SemaphoreSlim:

While concurrent execution is beneficial, there are scenarios where limiting the number of concurrent tasks is necessary to avoid overwhelming system resources. `SemaphoreSlim` is a synchronization primitive that can be used to limit concurrent access to a resource.

### Example: Limiting Concurrent Tasks with SemaphoreSlim

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

In this example, `SemaphoreSlim` is used to limit concurrent access to the `PerformTask` method. Only two tasks can run concurrently due to the semaphore limit, preventing excessive resource utilization.

## 3. Concurrent I/O Operations with async/await:

Asynchronous programming is highly beneficial for I/O-bound operations such as reading/writing files, accessing databases, or making network calls. Concurrent execution of I/O operations can significantly improve application responsiveness.

### Example: Concurrent File I/O Operations

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

### Example: Combining Concurrency and Error Handling

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

In this example, `Task.WhenAll` is combined with error handling using `try/catch`. If any operation throws an exception, it is captured in the `AggregateException`, allowing proper error reporting.

Implementing concurrent asynchronous operations is crucial for efficient resource utilization and improved application performance. Whether using `Task.WhenAll` for parallel execution, `SemaphoreSlim` for limiting concurrency, or combining async/await with I/O operations, understanding and leveraging these techniques can significantly enhance the responsiveness and scalability of applications. It's essential to consider the nature of tasks, resource constraints, and error handling strategies while designing concurrent asynchronous workflows in C# and .NET. Mastering these concepts empowers developers to build robust, high-performance applications that leverage the full potential of asynchronous programming.

## Leveraging asynchronous features in .NET libraries like HttpClient and Entity Framework Core 8 (if applicable)

Leveraging asynchronous features in .NET libraries like HttpClient and Entity Framework Core 6 (latest version at the time of writing) is crucial for building high-performance and scalable applications. Asynchronous programming allows these libraries to handle I/O-bound operations efficiently, such as making HTTP requests or accessing databases, without blocking the main thread. In this exploration, we will delve into how to leverage asynchronous features in these libraries using C# 12 and .NET 8, with code examples to demonstrate best practices.

### 1. Asynchronous HTTP Requests with HttpClient:

The `HttpClient` class in .NET is widely used for making HTTP requests to web APIs, and it provides asynchronous methods for efficient network communication. Asynchronous methods in `HttpClient` allow applications to perform non-blocking HTTP requests, improving responsiveness.

### Example: Making Asynchronous HTTP GET Request with HttpClient

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

In this example, `httpClient.GetAsync` is an asynchronous method that makes an HTTP GET request to the specified URL asynchronously. The `await` keyword is used to asynchronously wait for the response without blocking the main thread.

### 2. Asynchronous Database Operations with Entity Framework Core:

Entity Framework Core (EF Core) is a popular Object-Relational Mapping (ORM) framework in .NET for database access. EF Core supports asynchronous methods for database operations, allowing applications to perform database queries and updates asynchronously.

### Example: Asynchronous Query with Entity Framework Core

Assuming we have a `Post` entity and a `DbContext` setup:

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
