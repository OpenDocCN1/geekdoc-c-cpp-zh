
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
