# # 80. SERVERLESS COMPUTING WITH AZURE FUNCTIONS

Azure Functions allow you to run small units of code without managing infrastructure. You only pay for execution time.

Let’s write a simple Azure Function in C# that responds to an HTTP request.

[Code Example]

```
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
```