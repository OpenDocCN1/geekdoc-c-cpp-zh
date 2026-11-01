

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

## 第 7 章
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

