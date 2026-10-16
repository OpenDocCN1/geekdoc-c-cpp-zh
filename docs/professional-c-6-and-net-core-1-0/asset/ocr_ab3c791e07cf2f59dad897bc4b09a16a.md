method of the Startup class receives an ILoggerFactory object. With this interface you can add logger providers using the AddProvider method, and you create a logger implementing the ILogger interface with the CreateLogger method. The AddConsole and AddDebug methods shown in the following code snippet are extension methods to add different providers. The AddConsole method adds a provider to write log information to the console, the AddDebug method adds a provider to write log information to the debugger. Using both of these methods without passing argument values, a default is used to configure log messages. The default specifies to write log messages of type information and higher. You can use different overloads to specify other filters for logging, or you can use configuration files to configure logging (code file WebSampleApp/Startup.cs):

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    // etc.
    loggerFactory.AddConsole();
    loggerFactory.AddDebug();

    // etc.
}
```

With the ILogger interface you can write custom log information using the Log method.

# Adding Static Content

Usually you don’t want to just send simple strings to the client. By default, simple HTML files and other static content can’t be sent. ASP.NET 5 reduces the overhead as much as possible. Even static files are not returned from the server if you do not enable them.

To enable static files served from the web server, you can add the extension method UseStaticFiles (and comment the previously created Run method):

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    app.UseIISPlatformHandler();
    app.UseStaticFiles();

    //etc.
}
```

As soon as you add this code line with the same capitalization to the Configure method, the smart tag from the editor offers adding the NuGet package Microsoft.AspNet.StaticFiles. Select this, and the NuGet package is downloaded and listed in project.json:

```
"dependencies": {
    "Microsoft.AspNetCore.IISPlatformHandler":"1.0.0-*",
    "Microsoft.AspNetCore.Server.Kestrel":"1.0.0-*",
```