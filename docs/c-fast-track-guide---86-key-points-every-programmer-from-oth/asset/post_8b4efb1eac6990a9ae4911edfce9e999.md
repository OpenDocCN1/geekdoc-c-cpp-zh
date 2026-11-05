
```bash
docker build -t my-csharp-app .
```

### Run the container

```bash
docker run -d -p 8080:80 my-csharp-app
```

![](img/bb6e93ece31f33afd31e933e9dd494be_229_0.png)

### [Execution Result]

The ASP.NET Core app will be accessible at http://localhost:8080 inside the Docker container.

![](img/bb6e93ece31f33afd31e933e9dd494be_229_1.png)

- mcr.microsoft.com/dotnet/aspnet:6.0: Base runtime image.
- mcr.microsoft.com/dotnet/sdk:6.0: SDK used to build the app.
- The publish command compiles the app into the `/app` directory.
- The final image is lighter as it only contains what's necessary to run the app.

This separation into build and final stages is called multi-stage builds and keeps Docker images small and efficient.

By mapping port 8080 to the container's internal port 80, users can access the app in their browser.

![](img/bb6e93ece31f33afd31e933e9dd494be_229_2.png)

### [Supplement]

Docker ensures that the app runs the same way on any machine—perfect for microservices or cloud deployment. Visual Studio also includes Docker support with one-click integration. To verify if Docker is running: docker info or docker version.

![](img/bb6e93ece31f33afd31e933e9dd494be_231_0.png)

![](img/bb6e93ece31f33afd31e933e9dd494be_231_1.png)

![](img/bb6e93ece31f33afd31e933e9dd494be_231_2.png)

![](img/bb6e93ece31f33afd31e933e9dd494be_231_3.png)

## 79. Lightweight Web APIs with Minimal Code

Minimal APIs allow you to quickly build web endpoints in C# with minimal code. They’re ideal for microservices, small apps, and beginners exploring web development.

Here’s how to create a simple web API in C# using .NET’s Minimal API approach.

### [Code Example]

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

### [Execution Result]

When you run this application and access http://localhost:5000/ in your browser, it displays: Hello, World!

![](img/bb6e93ece31f33afd31e933e9dd494be_232_1.png)

This is the simplest form of a web API using Minimal APIs in .NET 6 or later. There is no need to create controllers or extra configuration files.

- `WebApplication.Create()` sets up a basic web host.
- `app.MapGet(...)` defines a route and its response.
- `app.Run()` starts the HTTP server.

Minimal APIs are great for quick prototyping or learning HTTP routes without boilerplate. However, they are also powerful enough to handle complex tasks, including middleware, dependency injection, and routing.

A beginner coming from another language should compare this with how endpoints are built in frameworks like Flask (Python) or Express (JavaScript) to see how concise and readable it is.

![](img/bb6e93ece31f33afd31e933e9dd494be_232_2.png)

### [Supplement]

- Minimal APIs were introduced in .NET 6.
- They reduce startup time and memory usage.
- Ideal for microservices or lightweight HTTP services.
- Can still use middleware, DI, and filters like full MVC.
- Great entry point for understanding HTTP methods in C#.

## 80. SERVERLESS COMPUTING WITH AZURE FUNCTIONS

Azure Functions allow you to run small units of code without managing infrastructure. You only pay for execution time.

Let’s write a simple Azure Function in C# that responds to an HTTP request.

### [Code Example]

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

### [Execution Result]

When this Azure Function is deployed and accessed, it returns: Hello from Azure Function!

Azure Functions use the serverless model. That means:

- You don’t manage any server or host.
- Your function is triggered by events (like HTTP requests, timers, queues).
- It automatically scales based on demand.

This example uses:

- `[Function("Function1")]` to mark it as an Azure Function.
- `[HttpTrigger(...)]` to declare that it responds to HTTP requests.
- `HttpRequestData` and `HttpResponseData` to work with the request and response.

While powerful, setting up Azure Functions requires understanding Azure’s ecosystem and tools like Azure CLI, Visual Studio Code, or the Azure Portal.

### [Supplement]

- Azure Functions support multiple languages: C#, JavaScript, Python, Java, and more.
- They're perfect for short-lived tasks like data transformation, webhooks, or automation.
- Pay-per-use: you’re billed only while your code runs.
- Functions can be deployed from Visual Studio or GitHub Actions.
- You can bind to many Azure services: Blob storage, Cosmos DB, Event Grid, etc.

## 81. SECURE API ACCESS WITH JWT IN C#

JWT (JSON Web Token) is a standard way to securely transmit information between parties, often used for authenticating users in APIs.

Here is a simple example of how to generate and validate a JWT in C# using the `System.IdentityModel.Tokens.Jwt` package.

### [Code Example]

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

### [Execution Result]

Generated JWT:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

Token is valid. User: JohnDoe

JWTs contain 3 parts: Header, Payload, and Signature.

- The Header includes the signing algorithm (e.g., HS256).
- The Payload holds claims (user info, expiration time).
- The Signature ensures the token hasn't been tampered with.
- JWTs are usually passed in HTTP headers as: `Authorization: Bearer <token>`.
- Validating a JWT checks its signature, expiration, and other claims.
- Do NOT hard-code secrets in production apps—use secure vaults or environment variables.

### [Supplement]

- JWTs are stateless: no session storage needed on server.
- The payload is Base64-encoded, not encrypted—never store sensitive data inside.
- You can decode JWTs using tools like jwt.io to inspect them manually.
