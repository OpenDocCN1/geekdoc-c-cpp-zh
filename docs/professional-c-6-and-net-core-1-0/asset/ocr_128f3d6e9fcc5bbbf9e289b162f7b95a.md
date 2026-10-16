```
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

Instead of using the Map method, you can also use MapWhen. With the following code snippet, the map managed by MapWhen applies when the path starts with /configuration. The remaining path is written to the variable remaining and can be used to differ with the method invocations:

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

Instead of just using the path, you can also access any other information of the HttpContext, such as the host information of the client (context.Request.Host) or authenticated users (context.User.Identity.IsAuthenticated).

# Using Middleware

ASP.NET Core makes it easy to create modules that are invoked before the controller is invoked. This can be used to add header information, verify tokens, build a cache, create log traces, and so on. One middleware module is chained after the other until all connected middleware types have been invoked.

You can create a middleware class by using the Visual Studio item template Middleware Class. With this middleware type, you create a constructor that receives a reference to the next middleware type. RequestDelegate is a delegate that receives an HttpContext as parameter and returns a Task. This is exactly the signature of the Invoke method. Within this method, you have access to request and response information. The type HeaderMiddleware adds a sample header to the response of the HttpContext. As the last action, the Invoke method invokes the next middleware module (code file WebSampleApp/Middleware/HeaderMiddleware.cs):

```
public class HeaderMiddleware
{
```