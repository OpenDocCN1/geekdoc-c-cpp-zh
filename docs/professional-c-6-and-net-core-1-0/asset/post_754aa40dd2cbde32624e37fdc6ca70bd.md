
extension method that can be called within the ConfigureServices method in the Startup class. The parameter enables you to configure the idle timeout and the cookie options. The cookie is used to identify the session. The session also makes use of a service that implements the interface IDistributedCache. A simple implementation is the cache for in-process session state. The method AddCaching adds the following cache service (code file WebSampleApp/Startup.cs):

```
public void ConfigureServices(IServiceCollection services)
{
    services.AddTransient<ISampleService, DefaultSampleService>();
    services.AddTransient<HomeController>();
    services.AddCaching();
    services.AddSession(options =>
        options.IdleTimeout = TimeSpan.FromMinutes(10));
}
```

> NOTE Other implementations of IDistributedCache are RedisCache and SqlServerCache in the NuGet packages Microsoft.Extensions.Caching.Redis and Microsoft.Extensions.Caching.SqlServer.

For using the session, you need to configure the session by calling the UseSession extension method. You need to invoke this method before any response is written to the response—such as is done with the UseHeaderMiddleware and UseHeading1Middleware—thus UseSession is called before the other methods. The code that uses session information is mapped to the /session path (code file WebSampleApp/Startup.cs):

```
public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
{
    // etc.
    app.UseSession();
    app.UseHeaderMiddleware();
    app.UseHeading1Middleware();

    app.Map("/session", sessionApp =>
    {
        sessionApp.Run(async context =>
        {
            await SessionSample.SessionAsync(context);
        });
    });
    // etc.
}
```

You can write session state using SetXXX methods, such as SetString and SetInt32. These methods are defined with the ISession interface that is returned from the Session property of the HttpContext. Session data is retrieved using GetXXX methods (code file WebSampleApp/SessionSample.cs):

```
public static class SessionSample
{
    private const string SessionVisits = nameof(SessionVisits);
    private const string SessionTimeCreated =
        nameof(SessionTimeCreated);

    public static async Task SessionAsync(HttpContext context)
    {
        int visits = context.Session.GetInt32(SessionVisits) ?? 0;
        string timeCreated =
            context.Session.GetString(SessionTimeCreated) ??
            string.Empty;
        if (string.IsNullOrEmpty(timeCreated))
        {
            timeCreated = DateTime.Now.ToString("t",
                CultureInfo.InvariantCulture);
            context.Session.SetString(SessionTimeCreated,
                timeCreated);
        }
        DateTime timeCreated2 = DateTime.Parse(timeCreated);
        context.Session.SetInt32(SessionVisits, ++visits);
        await context.Response.WriteAsync(
            $"Number of visits within this session: {visits}" +
            $"that was created at {timeCreated2:T};" +
            $"current time: {DateTime.Now:T}");
    }
}
```

> **NOTE** The sample code uses an invariant culture to store the time when the session was created. The time shown to the user is using a specific culture. It’s a good practice to use invariant cultures storing culture-specific data on the server. Information about invariant cultures and how to set cultures is explained in Chapter 28, “Localization.”

## Configuring ASP.NET

With web applications, it’s necessary to store configuration information that can be changed by system administrators—for example, connection strings. In the next chapter you create a data-driven application where a connection string is needed.

Configuration of ASP.NET Core 1.0 is no longer based on the XML configuration files web.config and machine.config as was the case with previous versions of ASP.NET. With the old configuration file, assembly references and assembly redirects were mixed with database connection strings and application settings. This is no longer the case. You’ve seen the project.json file to define assembly references. Connection strings and application settings are not defined there. Application settings are typically stored within appsettings.json, but the configuration is a lot more flexible and you can choose to make your configuration with several JSON or XML files and with environment variables.

A default ASP.NET configuration file—`appsettings.json`—is added from the item template ASP.NET Configuration File. The item template automatically creates the `DefaultConnection` setting; the `AppSettings` have been added later on (code file `WebSampleApp/appsettings.json`):

```json
{
  "AppSettings": {
    "SiteName":"Professional C# Sample"
  },
  "Data": {
    "DefaultConnection": {
      "ConnectionString": "Server=(localdb)\\MSSQLLocalDB;Database=_CHANGE_ME;Trusted_Connection=T;"
    }
  }
}
```

You need to configure the configuration file that’s used. You do this in the constructor of the `Startup` class. The `ConfigurationBuilder` class is used to build the configuration from configuration files. There can be more than one configuration file.

The sample code adds `appsettings.json` to the `ConfigurationBuilder` using the extension method `AddJsonFile`. After the setup of the configuration is done, the configuration files are read using the Build method. The returned `IConfigurationRoot` result is assigned to the read-only property `Configuration`, which makes it easy to read configuration information later on (code file `WebSampleApp/Startup.cs`):

```csharp
public Startup(IHostingEnvironment env)
{
    var builder = new ConfigurationBuilder()
        .AddJsonFile("appsettings.json");

    // etc.
    Configuration = builder.Build();
}

public IConfigurationRoot Configuration { get; }
// etc.
```

You can use the methods `AddXmlFile` to add an XML configuration file, `AddEnvironmentVariables` to add environment variables, and `AddCommandLine` to add command line arguments to the configuration.

For the configuration files, by default the current directory of the web application is used. In case you need to change the directory, you can invoke the method `SetBasePath` before invoking the method `AddJsonFile`. To retrieve the directory of the web application, you can inject the `IApplicationEnvironment` interface in the constructor and use the `ApplicationBasePath` property.

## Reading the Configuration

The different configuration values are read by mapping the `/configuration/appsettings`, `/configuration/database`, and `/configuration/secret` links (code file `WebSampleApp/Startup.cs`):

```
PathString remaining;
app.MapWhen(context =>
    context.Request.Path.StartsWithSegments("/configuration", out remaining),
    configApp =>
    {
        configApp.Run(async context =>
        {
            if (remaining.StartsWithSegments("/appsettings"))
            {
                await ConfigSample.AppSettings(context, Configuration);
            }
            else if (remaining.StartsWithSegments("/database"))
            {
                await ConfigSample.ReadDatabaseConnection(context, Configuration);
            }
            else if (remaining.StartsWithSegments("/secret"))
            {
                await ConfigSample.UserSecret(context, Configuration);
            }
        });
    });
```

The configuration can now be read by using the indexer of the IConfigurationRoot object. You can access the hierarchical elements of the JSON tree by using a colon (code file WebSampleApp/ConfigSample.cs):

```
public static async Task AppSettings(HttpContext context,
    IConfigurationRoot config)
{
    string settings = config["AppSettings:SiteName"];
    await context.Response.WriteAsync(settings.Div());
}
```

This is similar to accessing the database connection string:

```
public static async Task ReadDatabaseConnection(HttpContext context,
    IConfigurationRoot config)
{
    string connectionString =
config["Data:DefaultConnection:ConnectionString"];
    await context.Response.WriteAsync(connectionString.Div());
}
```

Running the web application accessing the corresponding /configuration URLs returns the values from the configuration file.

## Different Configurations Based on the Environment

When running your web application with different environments—for example, during development, testing, and production—you might also use a staging server because it’s likely you are using some different configurations. You don’t want to add test data to the production database.

ASP.NET 4 created transformations for XML files to define the differences from one configuration to the other. This can be done in a
