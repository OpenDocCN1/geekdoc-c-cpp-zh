![](bbox=[0.13, 0.12, 0.22, 0.15])

![](bbox=[0.48, 0.12, 0.58, 0.15])

![](bbox=[0.13, 0.16, 0.22, 0.19])

![](bbox=[0.13, 0.33, 0.22, 0.36])

# 79. Lightweight Web APIs with Minimal Code

Minimal APIs allow you to quickly build web endpoints in C# with minimal code. They’re ideal for microservices, small apps, and beginners exploring web development.

Here’s how to create a simple web API in C# using .NET’s Minimal API approach.

[Code Example]

```
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