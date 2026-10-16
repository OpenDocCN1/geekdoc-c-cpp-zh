
`Index` 方法接收一个 `HttpContext`，并利用它读取请求信息，同时返回一个 HTTP 状态值。在实现中，使用 `ISampleService` 从服务获取字符串。控制器添加一些 HTML 元素，将字符串放入列表中（代码文件 `WebSampleApp/Controllers/HomeController.cs`）：

```
public class HomeController
{
    private readonly ISampleService _service;
    public HomeController(ISampleService service)
    {
        _service = service;
    }

    public async Task<int> Index(HttpContext context)
    {
        var sb = new StringBuilder();
        sb.Append("<ul>");
        sb.Append(string.Join("",
            _service.GetSampleStrings().Select(
                s => $"<li>{s}</li>").ToArray()));
        sb.Append("</ul>");
        await context.Response.WriteAsync(sb.ToString());
        return 200;
    }
}
```

> **注意** *这个示例控制器直接返回 HTML 代码。更好的做法是将功能与用户界面分离，并由不同的类（视图）来生成 HTML 代码。为实现这种分离，最好使用框架：ASP.NET MVC。该框架将在第 41 章中介绍。*

## 调用控制器

要通过依赖注入实例化控制器，需要将 `HomeController` 类注册到 `IServiceCollection` 服务中。这一次你没有使用接口，因此只需通过 `AddTransient` 方法调用注册服务类型的具体实现（代码文件 `WebSampleApp/Startup.cs`）：

```
public void ConfigureServices(IServiceCollection services)
{
    services.AddTransient<ISampleService, DefaultSampleService>();
    services.AddTransient<HomeController>();
    // etc.
}
```

包含路由信息的 `Configure` 方法现在改为检查 `/home` 路径。如果该表达式返回 `true`，则通过调用已注册应用服务上的 `GetService` 方法，经由依赖注入实例化 `HomeController`。`IApplicationBuilder` 接口定义了一个 `ApplicationServices` 属性，该属性返回一个实现了 `IServiceProvider` 的对象。在这里，你可以访问所有已注册的服务。使用此控制器时，通过传递 `HttpContext` 调用 `Index` 方法。状态码会写入响应对象：

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    app.Run(async (context) =>
    {
        // etc.
        if (context.Request.Path.Value.ToLower() == "/home")
        {
            HomeController controller =
                app.ApplicationServices.GetService<HomeController>();
            int statusCode = await controller.Index(context);
            context.Response.StatusCode = statusCode;
            return;
        }
    });
    // etc.
}
```

[图 40.16](#figure-4016) 展示了当你使用指向主页地址的 URI 运行应用程序时，无序列表的输出。

![](img/3d365b72b289213a91ade7eb366b8f35_1553_0.png)

[图 40.16](#figure-4016)

## 使用 Map 进行路由

在前面的代码片段中，当 URL 的路径等于 `/home` 时，会调用 `HomeController` 类。你没有关注查询字符串或子文件夹。当然，你可以通过仅检查字符串的子集来实现这一点。然而，有一种更好的方法。ASP.NET 通过 `IApplicationBuilder` 的扩展支持子应用程序：`Map` 方法。

以下代码片段定义一个到 `/home2` 路径的映射，并运行 `HomeController` 的 `Invoke` 方法（代码文件 `WebSampleApp/Startup.cs`）：

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    // etc.
    app.Map("/home2", homeApp =>
    {
        homeApp.Run(async context =>
        {
            HomeController controller =
                app.ApplicationServices.GetService<HomeController>();
            int statusCode = await controller.Index(context);
            context.Response.StatusCode = statusCode;
        });
    });

    // etc.
}
```

除了使用 `Map` 方法，你还可以使用 `MapWhen`。在以下代码片段中，当路径以 `/configuration` 开头时，由 `MapWhen` 管理的映射将生效。剩余的路径会写入变量 `remaining`，并可用于区分方法调用：

```
PathString remaining;
app.MapWhen(context =>
    context.Request.Path.StartsWithSegments("/configuration", out remaining),
    configApp =>
    {
        configApp.Run(async context =>
        {
            // etc.
        }
    });
```

除了仅使用路径之外，你还可以访问 `HttpContext` 的任何其他信息，例如客户端的主机信息（`context.Request.Host`）或经过身份验证的用户（`context.User.Identity.IsAuthenticated`）。

## 使用中间件

ASP.NET Core 使得创建在控制器被调用之前调用的模块变得容易。这可用于添加头部信息、验证令牌、构建缓存、创建日志跟踪等。一个中间件模块接一个中间件模块地串联起来，直到所有连接的中间件类型都被调用。

你可以使用 Visual Studio 的项模板“中间件类”来创建中间件类。对于此中间件类型，你需要创建一个构造函数，它接收对下一个中间件类型的引用。`RequestDelegate` 是一个委托，它接收 `HttpContext` 作为参数并返回 `Task`。这正是 `Invoke` 方法的签名。在此方法中，你可以访问请求和响应信息。`HeaderMiddleware` 类型向 `HttpContext` 的响应添加一个示例头部。作为最后一个操作，`Invoke` 方法调用下一个中间件模块（代码文件 `WebSampleApp/Middleware/HeaderMiddleware.cs`）：

```
public class HeaderMiddleware
{
    private readonly RequestDelegate _next;

    public HeaderMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public Task Invoke(HttpContext httpContext)
    {
        httpContext.Response.Headers.Add("sampleheader",
            new string[] {"addheadermiddleware"});
        return _next(httpContext);
    }
}
```

为了方便配置中间件类型，扩展方法 `UseHeaderMiddleware` 扩展了 `IApplicationBuilder` 接口，并在其中调用了 `UseMiddleware` 方法：

```
public static class HeaderMiddlewareExtensions
{
    public static IApplicationBuilder UseHeaderMiddleware(
        this IApplicationBuilder builder) =>
            builder.UseMiddleware<HeaderMiddleware>();
}
```

另一个中间件类型是 `Heading1Middleware`。该类型与前面的中间件类型类似，它只是将一级标题写入响应中（代码文件 `WebSampleApp/Middleware/Heading1Middleware.cs`）：

```
public class Heading1Middleware
{
    private readonly RequestDelegate _next;

    public Heading1Middleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext httpContext)
    {
        await httpContext.Response.WriteAsync("<h1>From Middleware</h1>");
        await _next(httpContext);
    }
}
```

```
public static class Heading1MiddlewareExtensions
{
    public static IApplicationBuilder UseHeading1Middleware(
        this IApplicationBuilder builder) =>
            builder.UseMiddleware<Heading1Middleware>();
}
```

现在，配置所有中间件类型的工作由 `Startup` 类和 `Configure` 方法承担。扩展方法已经准备好供调用（代码文件 `WebSampleApp/Startup.cs`）：

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    // etc.
    app.UseHeaderMiddleware();
    app.UseHeading1Middleware();

    // etc.
}
```

当你运行应用程序时，你会看到返回给客户端的头部（使用浏览器的开发者工具），并且无论你使用之前创建的哪个链接，标题都会显示在每个页面上（参见图 40.17）。

![](img/3d365b72b289213a91ade7eb366b8f35_1556_0.png)

图 40.17

## 会话状态

使用中间件实现的服务是 *会话状态*。会话状态允许在服务器上临时记住来自客户端的数据。会话状态本身是作为中间件实现的。

当用户首次向服务器请求页面时，会话状态启动。当用户持续在服务器上打开页面时，会话会一直持续，直到发生超时（通常为 10 分钟）。为了在用户导航到新页面时在服务器上保持状态，可以将状态写入会话。当达到超时时间时，会话数据将被移除。

为了标识会话，在第一次请求时会创建一个包含会话标识符的临时 Cookie。该 Cookie 会在每次向服务器发出请求时从客户端返回，直到浏览器关闭，然后该 Cookie 被删除。作为使用 Cookie 的替代方案，会话标识符也可以放在 URL 字符串中发送。

在服务器端，会话信息可以存储在内存中。在 Web 场中，存储在内存中的会话状态不会在不同系统之间传播。通过粘性会话配置，用户始终返回同一台物理服务器。使用粘性会话时，其他系统上无法使用相同状态也没关系（除非某台服务器发生故障）。如果不用粘性会话，并且还要应对服务器故障，可以选择将会话状态存储在 SQL Server 数据库的分布式内存中。将会话状态存储在分布式内存中还有助于服务器进程的回收；即使你只使用单个服务器进程，回收也会破坏会话状态。

为了在 ASP.NET 中使用会话状态，你需要添加 NuGet 包 `Microsoft.AspNet.Session`。该包提供 `AddSession`
