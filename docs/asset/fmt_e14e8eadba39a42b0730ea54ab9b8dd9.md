

当你运行应用程序时，你会看到返回给客户端的头部（使用浏览器的开发者工具），并且无论你使用之前创建的哪个链接，标题都会显示在每个页面上（参见图 40.17）。

![](img/3d365b72b289213a91ade7eb366b8f35_1556_0.png)

图 40.17

### 会话状态

使用中间件实现的服务是 *会话状态*。会话状态允许在服务器上临时记住来自客户端的数据。会话状态本身是作为中间件实现的。

当用户首次向服务器请求页面时，会话状态启动。当用户持续在服务器上打开页面时，会话会一直持续，直到发生超时（通常为 10 分钟）。为了在用户导航到新页面时在服务器上保持状态，可以将状态写入会话。当达到超时时间时，会话数据将被移除。

为了标识会话，在第一次请求时会创建一个包含会话标识符的临时 Cookie。该 Cookie 会在每次向服务器发出请求时从客户端返回，直到浏览器关闭，然后该 Cookie 被删除。作为使用 Cookie 的替代方案，会话标识符也可以放在 URL 字符串中发送。

在服务器端，会话信息可以存储在内存中。在 Web 场中，存储在内存中的会话状态不会在不同系统之间传播。通过粘性会话配置，用户始终返回同一台物理服务器。使用粘性会话时，其他系统上无法使用相同状态也没关系（除非某台服务器发生故障）。如果不用粘性会话，并且还要应对服务器故障，可以选择将会话状态存储在 SQL Server 数据库的分布式内存中。将会话状态存储在分布式内存中还有助于服务器进程的回收；即使你只使用单个服务器进程，回收也会破坏会话状态。

为了在 ASP.NET 中使用会话状态，你需要添加 NuGet 包 `Microsoft.AspNet.Session`。该包提供`AddSession`扩展方法，可以在`Startup`类的`ConfigureServices`方法内调用。该参数使你可以配置空闲超时和cookie选项。该cookie用于标识会话。会话还使用了一个实现`IDistributedCache`接口的服务。一个简单的实现是进程内会话状态的缓存。`AddCaching`方法添加以下缓存服务（代码文件`WebSampleApp/Startup.cs`）：

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

> **注意** `IDistributedCache`的其他实现包括NuGet包`Microsoft.Extensions.Caching.Redis`和`Microsoft.Extensions.Caching.SqlServer`中的`RedisCache`和`SqlServerCache`。

要使用会话，你需要通过调用`UseSession`扩展方法来配置会话。你需要在向响应写入任何内容之前调用此方法——就像`UseHeaderMiddleware`和`UseHeading1Middleware`所做的那样——因此`UseSession`在其他方法之前调用。使用会话信息的代码被映射到`/session`路径（代码文件`WebSampleApp/Startup.cs`）：

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

你可以使用`SetXXX`方法写入会话状态，例如`SetString`和`SetInt32`。这些方法定义在从`HttpContext`的`Session`属性返回的`ISession`接口上。会话数据使用`GetXXX`方法检索（代码文件`WebSampleApp/SessionSample.cs`）：

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

> **注意** 示例代码使用固定区域性来存储会话创建的时间。显示给用户的时间使用特定区域性。在服务器上存储特定区域性数据时，使用固定区域性是一种很好的做法。有关固定区域性以及如何设置区域性的信息，请参阅第28章“本地化”。

### 配置ASP.NET

对于Web应用程序，有必要存储可由系统管理员更改的配置信息——例如，连接字符串。在下一章中，你将创建一个需要连接字符串的数据驱动应用程序。

ASP.NET Core 1.0的配置不再像之前版本的ASP.NET那样基于XML配置文件`web.config`和`machine.config`。在旧的配置文件中，程序集引用和程序集重定向与数据库连接字符串和应用程序设置混在一起。现在情况不再如此。你已经看到了用于定义程序集引用的`project.json`文件。连接字符串和应用程序设置不在那里定义。应用程序设置通常存储在`appsettings.json`中，但配置更加灵活，你可以选择使用多个JSON或XML文件以及环境变量进行配置。

默认的ASP.NET配置文件——`appsettings.json`——从项模板“ASP.NET配置文件”添加。该项模板会自动创建`DefaultConnection`设置；`AppSettings`是后来添加的（代码文件`WebSampleApp/appsettings.json`）：

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

你需要配置所使用的配置文件。可以在`Startup`类的构造函数中完成。`ConfigurationBuilder`类用于从配置文件构建配置。配置文件可以有多个。

示例代码使用扩展方法`AddJsonFile`将`appsettings.json`添加到`ConfigurationBuilder`中。配置设置完成后，使用`Build`方法读取配置文件。返回的`IConfigurationRoot`结果被赋给只读属性`Configuration`，这便于稍后读取配置信息（代码文件`WebSampleApp/Startup.cs`）：

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

你可以使用`AddXmlFile`方法添加XML配置文件，使用`AddEnvironmentVariables`方法添加环境变量，使用`AddCommandLine`方法向配置添加命令行参数。

对于配置文件，默认使用Web应用程序的当前目录。如果你需要更改目录，可以在调用`AddJsonFile`方法之前调用`SetBasePath`方法。要获取Web应用程序的目录，可以在构造函数中注入`IApplicationEnvironment`接口，并使用`ApplicationBasePath`属性。

### 读取配置

通过映射`/configuration/appsettings`、`/configuration/database`和`/configuration/secret`链接来读取不同的配置值（代码文件`WebSampleApp/Startup.cs`）：

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

现在可以使用`IConfigurationRoot`对象的索引器读取配置。你可以通过冒号访问JSON树的层次结构元素（代码文件`WebSampleApp/ConfigSample.cs`）：

```

public static async Task AppSettings(HttpContext context,

    IConfigurationRoot config)

{

    string settings = config["AppSettings:SiteName"];

    await context.Response.WriteAsync(settings.Div());

}

```

这类似于访问数据库连接字符串：

```

public static async Task ReadDatabaseConnection(HttpContext context,

    IConfigurationRoot config)

{

    string connectionString =

config["Data:DefaultConnection:ConnectionString"];

    await context.Response.WriteAsync(connectionString.Div());

}

```

运行Web应用程序并访问相应的`/configuration` URL，将返回配置文件中的值。

### 基于环境的不同配置

在不同的环境中运行Web应用程序时——例如，在开发、测试和生产期间——你可能还会使用暂存服务器，因为你可能正在使用一些不同的配置。你不会希望将测试数据添加到生产数据库中。

ASP.NET 4为XML文件创建了转换，以定义一个配置与另一个配置之间的差异。这可以在一个

使用 ASP.NET Core 1.0 有一种更简单的方式。对于应该不同的配置值，你可以使用不同的配置文件。

下面的代码片段添加了带有环境名称的 JSON 配置文件——例如，`appsettings.development.json` 或 `appsettings.production.json`（代码文件`WebSampleApp/Startup.cs`）：

```

var builder = new ConfigurationBuilder()

    .AddJsonFile("appsettings.json")

    .AddJsonFile($"appsettings.{env.EnvironmentName}.json", optional: true);

```

你可以通过设置环境变量或在项目属性中设置应用程序参数来配置环境，如图 40.18 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1561_0.png)

**图 40.18**

要以编程方式验证托管环境，可以为`IHostingEnvironment`定义扩展方法，例如`IsDevelopment`、`IsStaging`和`IsProduction`。要测试任何环境名称，你可以向`IsEnvironment`传递一个验证字符串：

```

if (env.IsDevelopment())

{

    // 等等

}

```

#### 用户机密

只要使用 Windows 身份验证，配置文件中包含连接字符串并不是什么大问题。当你将用户名和密码与连接字符串一起存储时，将连接字符串添加到配置文件并将配置文件与源代码存储库一起存储可能会成为一个大问题。拥有公共存储库并将 Amazon 密钥与配置一起存储可能会导致迅速损失数千美元。黑客的后台任务会扫描公共 GitHub 存储库，以查找 Amazon 密钥来劫持账户并创建虚拟机来挖掘比特币。你可以阅读 http://readwrite.com/2014/04/15/amazon-web-services-hack-bitcoin-miners-github 来了解更多关于这种情况的信息。

ASP.NET Core 1.0 对此有一些缓解措施：用户机密。使用用户机密，配置不会存储在项目的配置文件中；它存储在与你的账户关联的配置文件中。

安装 Visual Studio 时，`SecretManager`已经安装在你的系统上。在其他系统上，你需要安装 NuGet 包`Microsoft.Extensions.SecretManager`。

在`SecretManager`安装完成并且使用应用程序定义了机密之后，你可以使用命令行工具`user-secret`来设置、删除和列出应用程序中的用户机密。

机密存储在此用户特定的位置：

```

%AppData%\Microsoft\UserSecrets

```

管理用户机密的一种简单方法是从 Visual Studio 的解决方案资源管理器中进行。选择项目节点并打开上下文菜单，选择“管理用户机密”。当你第一次在项目中选择此项时，它会向`project.json`添加一个机密标识符（代码文件`WebSampleApp/project.json`）：

```

"userSecretsId": "aspnet5-WebSampleApp-20151215011720"

```

