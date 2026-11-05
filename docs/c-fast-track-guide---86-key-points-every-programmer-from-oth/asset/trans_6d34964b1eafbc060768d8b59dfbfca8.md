
```bash
docker build -t my-csharp-app .
```

### 运行容器

```bash
docker run -d -p 8080:80 my-csharp-app
```

![](img/bb6e93ece31f33afd31e933e9dd494be_229_0.png)

### [执行结果]

ASP.NET Core 应用将在 Docker 容器内通过 http://localhost:8080 访问。

![](img/bb6e93ece31f33afd31e933e9dd494be_229_1.png)

- mcr.microsoft.com/dotnet/aspnet:6.0：基础运行时镜像。
- mcr.microsoft.com/dotnet/sdk:6.0：用于构建应用的 SDK。
- publish 命令将应用编译到 `/app` 目录。
- 最终镜像更轻量，因为它只包含运行应用所需的组件。

这种将构建阶段和最终阶段分离的做法称为多阶段构建，可使 Docker 镜像保持小巧高效。

通过将 8080 端口映射到容器内部的 80 端口，用户可以在浏览器中访问应用。

![](img/bb6e93ece31f33afd31e933e9dd494be_229_2.png)

### [补充]

Docker 确保应用在任何机器上以相同方式运行——非常适合微服务或云部署。Visual Studio 也提供了一键集成的 Docker 支持。要验证 Docker 是否正在运行：docker info 或 docker version。

![](img/bb6e93ece31f33afd31e933e9dd494be_231_0.png)

![](img/bb6e93ece31f33afd31e933e9dd494be_231_1.png)

![](img/bb6e93ece31f33afd31e933e9dd494be_231_2.png)

![](img/bb6e93ece31f33afd31e933e9dd494be_231_3.png)

## 79. 使用极简代码构建轻量级 Web API

Minimal APIs 允许你用最少的代码快速在 C# 中构建 Web 端点。它们非常适合微服务、小型应用以及探索 Web 开发的初学者。

下面介绍如何使用 .NET 的 Minimal API 方法在 C# 中创建一个简单的 Web API。

### [代码示例]

```csharp
// Program.cs

// Import the necessary namespace
using Microsoft.AspNetCore.Builder;

using Microsoft.AspNetCore.Http;

var app = WebApplication.Create(); // Create the web application instance

// Define a GET endpoint for the root URL "/"
app.MapGet("/", () => "Hello, World!");

// Start the app
app.Run();
```

![](img/bb6e93ece31f33afd31e933e9dd494be_232_0.png)

### [执行结果]

当你运行此应用程序并在浏览器中访问 http://localhost:5000/ 时，它会显示：Hello, World！

![](img/bb6e93ece31f33afd31e933e9dd494be_232_1.png)

这是使用 .NET 6 或更高版本中 Minimal APIs 的最简单形式的 Web API。无需创建控制器或额外的配置文件。

- `WebApplication.Create()` 设置一个基础 Web 主机。
- `app.MapGet(...)` 定义路由及其响应。
- `app.Run()` 启动 HTTP 服务器。

Minimal APIs 非常适合快速原型设计或在没有样板代码的情况下学习 HTTP 路由。然而，它们也足够强大，可以处理复杂任务，包括中间件、依赖注入和路由。

来自其他语言的初学者应将其与 Flask（Python）或 Express（JavaScript）等框架中端点的构建方式进行比较，以了解其简洁性和可读性。

![](img/bb6e93ece31f33afd31e933e9dd494be_232_2.png)

### [补充]

- Minimal APIs 在 .NET 6 中引入。
- 它们可减少启动时间和内存使用。
- 非常适合微服务或轻量级 HTTP 服务。
- 仍可像完整的 MVC 一样使用中间件、DI 和过滤器。
- 了解 C# 中 HTTP 方法的绝佳切入点。

## 80. 使用 Azure Functions 进行无服务器计算

Azure Functions 允许你在无需管理基础设施的情况下运行小型代码单元。你只需为执行时间付费。

让我们编写一个简单的 Azure Function C# 代码，使其响应 HTTP 请求。

### [代码示例]

```csharp
// Function1.cs
using System.Net;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
public class Function1
{
    private readonly ILogger _logger;
    public Function1(ILoggerFactory loggerFactory)
    {
        _logger = loggerFactory.CreateLogger<Function1>();
    }
    [Function("Function1")]
    public HttpResponseData Run(
        [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
    {
        _logger.LogInformation("HTTP trigger function processed a request.");
        var response = req.CreateResponse(HttpStatusCode.OK);
        response.WriteString("Hello from Azure Function!");
        return response;
    }
}
```

### [执行结果]

当此 Azure Function 部署并访问时，它返回：Hello from Azure Function！

Azure Functions 使用无服务器模型。这意味着：

- 你无需管理任何服务器或主机。
- 你的函数由事件触发（如 HTTP 请求、计时器、队列）。
- 它会根据需求自动扩展。

此示例使用：

- `[Function("Function1")]` 将其标记为 Azure Function。
- `[HttpTrigger(...)]` 声明它响应 HTTP 请求。
- `HttpRequestData` 和 `HttpResponseData` 用于处理请求和响应。

虽然功能强大，但设置 Azure Functions 需要了解 Azure 生态系统以及 Azure CLI、Visual Studio Code 或 Azure Portal 等工具。

### [补充]

- Azure Functions 支持多种语言：C#、JavaScript、Python、Java 等。
- 它们非常适合数据转换、Webhooks 或自动化等短时任务。
- 按需付费：仅在代码运行时计费。
- 函数可以从 Visual Studio 或 GitHub Actions 部署。
- 你可以绑定到许多 Azure 服务：Blob 存储、Cosmos DB、Event Grid 等。

## 81. 使用 JWT 在 C# 中实现安全的 API 访问

JWT（JSON Web Token）是一种在各方之间安全传输信息标准，通常用于 API 中的用户身份验证。

下面是一个使用 `System.IdentityModel.Tokens.Jwt` 包在 C# 中生成和验证 JWT 的简单示例。

### [代码示例]

```csharp
// Install the following NuGet packages first:
// - System.IdentityModel.Tokens.Jwt
// - Microsoft.IdentityModel.Tokens

using System;
using System.Text;
using System.IdentityModel.Tokens.Jwt;
using Microsoft.IdentityModel.Tokens;
using System.Security.Claims;
class Program
{
    static void Main()
    {
        // Secret key (keep this safe in real apps!)
        var secretKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("SuperSecretKey12345"));
        // Sign credentials using HMAC SHA256
        var signingCredentials = new SigningCredentials(secretKey, SecurityAlgorithms.HmacSha256);
        // Define the token content (claims)
        var tokenDescriptor = new JwtSecurityToken(
            issuer: "myApp",
            audience: "myUsers",
            claims: new[] { new Claim(ClaimTypes.Name, "JohnDoe") },
            expires: DateTime.UtcNow.AddMinutes(30),
            signingCredentials: signingCredentials
        );

        // Create the token
        var tokenHandler = new JwtSecurityTokenHandler();
        var tokenString = tokenHandler.WriteToken(tokenDescriptor);
        Console.WriteLine("Generated JWT:");
        Console.WriteLine(tokenString);

        // ===== VALIDATION =====
        var tokenValidationParams = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidIssuer = "myApp",
            ValidAudience = "myUsers",
            IssuerSigningKey = secretKey
        };
        try
        {
            var principal = tokenHandler.ValidateToken(tokenString, tokenValidationParams, out var validatedToken);
            Console.WriteLine("Token is valid. User: " + principal.Identity.Name);
        }
        catch (Exception ex)
        {
            Console.WriteLine("Invalid token: " + ex.Message);
        }
    }
}
```

### [执行结果]

Generated JWT:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Token is valid. User: JohnDoe

JWT 包含 3 部分：Header、Payload 和 Signature。

- Header 包含签名算法（例如 HS256）。
- Payload 包含声明（用户信息、过期时间）。
- Signature 确保令牌未被篡改。
- JWT 通常作为 HTTP 头部传递：`Authorization: Bearer <token>`。
- 验证 JWT 会检查其签名、过期时间和其他声明。
- 不要在生产应用中硬编码密钥——请使用安全保管库或环境变量。

### [补充]

- JWT 是无状态的：服务器无需会话存储。
- 负载是 Base64 编码的，而非加密——切勿在其中存储敏感数据。
- 你可以使用 jwt.io 等工具解码 JWT 以手动检查它们。

