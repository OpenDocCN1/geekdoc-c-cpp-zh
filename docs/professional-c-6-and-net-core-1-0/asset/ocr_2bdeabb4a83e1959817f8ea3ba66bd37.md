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

# Different Configurations Based on the Environment

When running your web application with different environments—for example, during development, testing, and production—you might also use a staging server because it’s likely you are using some different configurations. You don’t want to add test data to the production database.

ASP.NET 4 created transformations for XML files to define the differences from one configuration to the other. This can be done in a