

# web.config 文件中 session state 元素的属性

| Attribute | Description |
|---|---|
| Mode | 会话状态模式。可选值为 Off、InProc、StateServer、SQLServer 或 Custom。默认值为 InProc。 |
| Cookieless | 一个 HttpCookieMode 值，指定是否使用无 Cookie 会话。AutoDetect 如果支持则使用 Cookie，如果不支持则使用查询字符串。UseUri 使用查询字符串。默认值为 UseCookies。 |
| Timeout | 会话在无用户活动的情况下应保持的分钟数。默认值为 20。 |
| StateConnectionString | 运行 ASP.NET 状态服务的服务器的名称或 IP 地址以及端口号（始终为 42424）。在使用 State Server 模式时，此属性为必需。 |
| SqlConnectionString | 用于存储会话状态数据的 SQL Server 实例的连接字符串。如果 allowCustomSqlDatabase 属性设置为 True，连接字符串还可以包含数据库的名称。在使用 SQL Server 模式时，此属性为必需。 |
| AllowCustomSqlDatabase | 一个布尔值，确定 SqlConnectionString 是否可以指定用于存储状态信息的数据库的名称。默认值是 False，在这种情况下，状态信息存储在名为 ASPState 的数据库中。 |
| CustomProvider | 自定义会话状态存储提供程序的名称。 |
| CompressionEnabled | 一个布尔值，确定是否压缩未存储在进程内的会话状态数据。默认值为 False。 |

## 使用进程内模式的 web.config 文件中的 sessionState 元素

```
<?xml version="1.0"?>
<configuration>
  <system.web>
    .
    .
    <sessionState mode="InProc"
      cookieless="AutoDetect"
      timeout="30"
    />
    .
    .
  </system.web>
</configuration>
```

## Description

- web.config 文件包含影响 ASP.NET Web 应用程序运行方式的设置。要更改会话状态的默认选项，可以向 web.config 文件添加 sessionState 元素，然后指定要使用的属性和值。
- 在使用 SQL Server 模式之前，必须创建将用于存储会话状态数据的数据库。有关如何执行此操作的说明，请参阅帮助文档中的“Session-State Modes”主题。
- 如果指定 Custom 模式，必须在 web.config 文件中包含其他信息以标识会话状态存储提供程序。有关更多信息，请参阅帮助文档中的“Session-State Modes”主题。

## How to use application state

与存储单个用户会话数据的会话状态不同，应用程序状态允许您存储由应用程序的所有用户共享的数据。在接下来的主题中，您将学习如何使用应用程序状态。

### How application state works

图 8-7 介绍了使用 *应用程序状态* 所需的概念。首先，*应用程序* 由位于 IIS Web 服务器单个目录下的所有页面、代码和其他文件组成。

当用户首次请求位于应用程序目录中的页面时，ASP.NET 初始化应用程序。在此过程中，ASP.NET 从 HttpApplication 类创建一个 *应用程序对象*。该对象由一个名为 global.asax 的特殊类文件表示，您将在图 8-9 中学习如何使用它。

应用程序对象可以被应用程序的任何页面访问。该对象一直存在直到应用程序结束，这通常不会发生，直到 IIS 关闭为止。但是，每次重建应用程序或编辑应用程序的 web.config 文件时，应用程序都会自动重新启动。

每次 ASP.NET 启动应用程序并创建应用程序对象时，它还会从 HttpApplicationState 类创建一个 *应用程序状态对象*。您可以使用此对象在服务器内存中存储数据，该数据可被应用程序的任何页面访问。

应用程序状态通常用于存储不经常更改的特定于应用程序的数据。例如，您可能会使用应用程序状态来存储订购系统的折扣条款和税率。虽然您可以在每次需要时从数据库检索此类信息，但在应用程序启动时仅检索一次然后存储在应用程序状态中有时更有意义。这样，数据在应用程序执行时更容易访问。

尽管不太常见，但应用程序状态也可以用于存储每次用户访问站点或站点内的页面时都会更改的信息。例如，您可以使用它来跟踪登录提供聊天室或论坛的应用程序的用户。您还可以使用它来存储命中计数器，以跟踪用户检索特定页面的次数。例如，本图顶部的 Counter 应用程序跟踪所有应用程序用户点击 Post 按钮的次数。这与您在图 8-4 中看到的应用程序类似，但该应用程序使用会话状态来跟踪单个用户的计数。

## 一个计数所有用户点击按钮次数的 Counter 应用程序

![](img/c024ccf88e28c30c07dd410d4342288f_314_0.png)

## Application concepts

- ASP.NET *应用程序* 是 Web 服务器上单个目录内的页面、代码和其他文件的集合。在大多数情况下，ASP.NET 应用程序对应于单个 Visual Studio Web 项目。
- 应用程序从第一个用户请求应用程序的一部分页面时开始。然后，ASP.NET 在处理页面请求之前初始化应用程序。
- 作为初始化的一部分，ASP.NET 从 HttpApplication 类创建一个 *应用程序对象*。该对象存在于应用程序的整个生命周期中。您可以使用 global.asax 文件来使用应用程序对象，如图 8-9 中所述。
- 一旦应用程序启动，它通常不会在 Web 服务器关闭之前结束。但是，如果您重建应用程序或编辑 web.config 文件，则下次用户请求应用程序的一部分页面时，应用程序将被重新启动。

## Application state concepts

- 如果您将项目存储在 *应用程序状态* 中，则这些项目可供应用程序的所有用户使用。
- 为了提供应用程序状态的使用，ASP.NET 为每个应用程序从 HttpApplicationState 类创建一个 *应用程序状态对象*，并将此对象存储在服务器内存中。
- 应用程序状态通常用于存储不经常更改的数据，但也可以用于存储应用程序执行时更改的数据。

## How to work with application state data

图 8-8 介绍了使用应用程序状态数据的详细信息。正如前三个示例所示，您将项目添加到应用程序状态以及从应用程序状态检索项目所使用的技术与您用于处理会话状态中的项目所使用的技术类似。主要区别在于，您使用页面的 Application 属性从代码隐藏文件访问应用程序状态对象，并且您使用当前请求的 HttpContext 对象的 Application 属性从代码隐藏文件以外的类访问应用程序状态对象。

当您使用应用程序状态数据时，在修改其任何数据时，您需要锁定应用程序状态集合。这在该图中的最后一个示例中有所说明，该示例将名为 ClickCount 的应用程序状态项递增一。在这里，应用程序状态集合在检索 ClickCount 项之前被锁定。然后，在更新该项后，应用程序状态集合被解锁。为了最大限度地减少应用程序状态对象被锁定的时间，您应该在 Lock 和 Unlock 方法之间尽可能少地进行处理。

如果在更新计数时不锁定应用程序状态集合，则两个或多个用户可能同时访问该计数。为了说明这为什么是个问题，让我们假设三个用户同时访问计数项，并且起始计数为 11。然后，当每个用户递增计数时，它变为 12，并且每个用户将该值存储在应用程序状态集合中。在这种情况下，正确的计数应该是 14。

