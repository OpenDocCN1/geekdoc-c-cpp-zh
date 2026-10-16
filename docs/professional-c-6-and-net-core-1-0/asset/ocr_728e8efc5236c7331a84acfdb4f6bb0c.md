controller, the `Index` method is invoked by passing the `HttpContext`. The status code is written to the response object:

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

[Figure 40.16](#figure-4016) shows the output of the unordered list when you run the application with a URI to the home address.

![](bbox=[0.106, 0.399, 0.895, 0.581])

[Figure 40.16](#figure-4016)

# Routing Using Map

With the previous code snippet, the `HomeController` class was invoked when the path of the URL equals `/home`. You didn’t pay attention to query strings or subfolders. Of course, you could do this by checking only a subset of the string. However, there’s a much better way. ASP.NET supports subapplications with an extension of the `IApplicationBuilder`: the `Map` method.

The following code snippet defines a map to the `/home2` path and runs the `Invoke` method of the `HomeController` (code file `WebSampleApp/Startup.cs`):

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    // etc.
    app.Map("/home2", homeApp =>
    {
```