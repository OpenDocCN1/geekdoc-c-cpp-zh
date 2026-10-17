
请注意，连接字符串中不包含数据库，这意味着使用名为 `ASPState` 的默认数据库。如果你想使用不同的数据库来存储会话状态数据，你需要在连接字符串中包含数据库的名称，并且你需要包含 `allowCustomSqlDatabase` 属性，其值为 `True`。

如果你使用除 in-process 之外的任何模式，还可以通过将 `compressionEnabled` 属性设置为 `True` 来压缩会话状态数据。这是 ASP.NET 4 的新功能，可以使将数据传递到另一台服务器或数据库更有效。

## web.config 文件中 session state 元素的属性

| Attribute | Description |
|---|---|
| `Mode` | 会话状态模式。可选值为 `Off`、`InProc`、`StateServer`、`SQLServer` 或 `Custom`。默认值为 `InProc`。 |
| `Cookieless` | 一个 `HttpCookieMode` 值，指定是否使用无 Cookie 会话。`AutoDetect` 如果支持则使用 Cookie，如果不支持则使用查询字符串。`UseUri` 使用查询字符串。默认值为 `UseCookies`。 |
| `Timeout` | 会话在无用户活动的情况下应保持的分钟数。默认值为 20。 |
| `StateConnectionString` | 运行 ASP.NET 状态服务的服务器的名称或 IP 地址以及端口号（始终为 42424）。在使用 `State Server` 模式时，此属性为必需。 |
| `SqlConnectionString` | 用于存储会话状态数据的 SQL Server 实例的连接字符串。如果 `allowCustomSqlDatabase` 属性设置为 `True`，连接字符串还可以包含数据库的名称。在使用 SQL Server 模式时，此属性为必需。 |
| `AllowCustomSqlDatabase` | 一个布尔值，确定 `SqlConnectionString` 是否可以指定用于存储状态信息的数据库的名称。默认值是 `False`，在这种情况下，状态信息存储在名为 `ASPState` 的数据库中。 |
| `CustomProvider` | 自定义会话状态存储提供程序的名称。 |
| `CompressionEnabled` | 一个布尔值，确定是否压缩未存储在进程内的会话状态数据。默认值为 `False`。 |

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

- `web.config` 文件包含影响 ASP.NET Web 应用程序运行方式的设置。要更改会话状态的默认选项，可以向 `web.config` 文件添加 `sessionState` 元素，然后指定要使用的属性和值。
- 在使用 SQL Server 模式之前，必须创建将用于存储会话状态数据的数据库。有关如何执行此操作的说明，请参阅帮助文档中的“Session-State Modes”主题。
- 如果指定 `Custom` 模式，必须在 `web.config` 文件中包含其他信息以标识会话状态存储提供程序。有关更多信息，请参阅帮助文档中的“Session-State Modes”主题。

## How to use application state

与存储单个用户会话数据的会话状态不同，应用程序状态允许您存储由应用程序的所有用户共享的数据。在接下来的主题中，您将学习如何使用应用程序状态。

## How application state works

图 8-7 介绍了使用 *应用程序状态* 所需的概念。首先，*应用程序* 由位于 IIS Web 服务器单个目录下的所有页面、代码和其他文件组成。

当用户首次请求位于应用程序目录中的页面时，ASP.NET 初始化应用程序。在此过程中，ASP.NET 从 `HttpApplication` 类创建一个 *应用程序对象*。该对象由一个名为 `global.asax` 的特殊类文件表示，您将在图 8-9 中学习如何使用它。

应用程序对象可以被应用程序的任何页面访问。该对象一直存在直到应用程序结束，这通常不会发生，直到 IIS 关闭为止。但是，每次重建应用程序或编辑应用程序的 `web.config` 文件时，应用程序都会自动重新启动。

每次 ASP.NET 启动应用程序并创建应用程序对象时，它还会从 `HttpApplicationState` 类创建一个 *应用程序状态对象*。您可以使用此对象在服务器内存中存储数据，该数据可被应用程序的任何页面访问。

应用程序状态通常用于存储不经常更改的特定于应用程序的数据。例如，您可能会使用应用程序状态来存储订购系统的折扣条款和税率。虽然您可以在每次需要时从数据库检索此类信息，但在应用程序启动时仅检索一次然后存储在应用程序状态中有时更有意义。这样，数据在应用程序执行时更容易访问。

尽管不太常见，但应用程序状态也可以用于存储每次用户访问站点或站点内的页面时都会更改的信息。例如，您可以使用它来跟踪登录提供聊天室或论坛的应用程序的用户。您还可以使用它来存储命中计数器，以跟踪用户检索特定页面的次数。例如，本图顶部的 Counter 应用程序跟踪所有应用程序用户点击 Post 按钮的次数。这与您在图 8-4 中看到的应用程序类似，但该应用程序使用会话状态来跟踪单个用户的计数。

## 一个计数所有用户点击按钮次数的 Counter 应用程序

![](img/c024ccf88e28c30c07dd410d4342288f_314_0.png)

## Application concepts

- ASP.NET *应用程序* 是 Web 服务器上单个目录内的页面、代码和其他文件的集合。在大多数情况下，ASP.NET 应用程序对应于单个 Visual Studio Web 项目。
- 应用程序从第一个用户请求应用程序的一部分页面时开始。然后，ASP.NET 在处理页面请求之前初始化应用程序。
- 作为初始化的一部分，ASP.NET 从 `HttpApplication` 类创建一个 *应用程序对象*。该对象存在于应用程序的整个生命周期中。您可以使用 `global.asax` 文件来使用应用程序对象，如图 8-9 中所述。
- 一旦应用程序启动，它通常不会在 Web 服务器关闭之前结束。但是，如果您重建应用程序或编辑 `web.config` 文件，则下次用户请求应用程序的一部分页面时，应用程序将被重新启动。

## Application state concepts

- 如果您将项目存储在 *应用程序状态* 中，则这些项目可供应用程序的所有用户使用。
- 为了提供应用程序状态的使用，ASP.NET 为每个应用程序从 `HttpApplicationState` 类创建一个 *应用程序状态对象*，并将此对象存储在服务器内存中。
- 应用程序状态通常用于存储不经常更改的数据，但也可以用于存储应用程序执行时更改的数据。

## How to work with application state data

图 8-8 介绍了使用应用程序状态数据的详细信息。正如前三个示例所示，您将项目添加到应用程序状态以及从应用程序状态检索项目所使用的技术与您用于处理会话状态中的项目所使用的技术类似。主要区别在于，您使用页面的 `Application` 属性从代码隐藏文件访问应用程序状态对象，并且您使用当前请求的 `HttpContext` 对象的 `Application` 属性从代码隐藏文件以外的类访问应用程序状态对象。

当您使用应用程序状态数据时，在修改其任何数据时，您需要锁定应用程序状态集合。这在该图中的最后一个示例中有所说明，该示例将名为 `ClickCount` 的应用程序状态项递增一。在这里，应用程序状态集合在检索 `ClickCount` 项之前被锁定。然后，在更新该项后，应用程序状态集合被解锁。为了最大限度地减少应用程序状态对象被锁定的时间，您应该在 `Lock` 和 `Unlock` 方法之间尽可能少地进行处理。

如果在更新计数时不锁定应用程序状态集合，则两个或多个用户可能同时访问该计数。为了说明这为什么是个问题，让我们假设三个用户同时访问计数项，并且起始计数为 11。然后，当每个用户递增计数时，它变为 12，并且每个用户将该值存储在应用程序状态集合中。在这种情况下，正确的计数应该是 14。

## HttpApplicationState 类的常用成员

| Indexer | Description |
|---|---|
| `[name]` | 具有指定名称的应用程序状态项的值。如果设置不存在的项的值，则会创建该项。 |
| Property | Description |
| `Count` | 应用程序状态集合中的项数。 |
| Method | Description |
| `Add(name, value)` | 向应用程序状态集合添加一项。 |
| `Clear()` | 从应用程序状态集合中移除所有项。 |
| `Remove(name)` | 从应用程序状态集合中移除具有指定名称的项。 |
| `Lock()` | 锁定应用程序状态集合，使只有当前用户可以访问它。 |
| `Unlock()` | 解锁应用程序状态集合，使其他用户可以访问它。 |

## 从应用程序状态检索项的语句

```
int applicationCount = Convert.ToInt32(Application["ClickCount"]);
```

## 向应用程序状态添加项的语句

```
Application.Add("ClickCount", 0);
```

## 从非页面类检索应用程序状态的语句

```
int applicationCount = Convert.ToInt32
(HttpContext.Current.Application["ClickCount"]);
```

## 检索和更新项时锁定应用程序状态的代码

```
Application.Lock();
int applicationCount = Convert.ToInt32(Application["ClickCount"]);
applicationCount++;
Application["ClickCount"] = applicationCount;
Application.Unlock();
```

## Description

- 你可以使用应用程序状态对象来存储对应用程序所有用户都通用的项。
- 要从 ASP.NET Web 窗体的代码隐藏文件中访问应用程序状态对象，请使用页面的 `Application` 属性。
- 要从代码隐藏文件以外的类访问应用程序状态对象，请使用 `HttpContext` 类的 `Current` 属性获取当前请求的 `HttpContext` 对象。然后，使用此对象的 `Application` 属性获取应用程序状态对象。
- 在检索你打算修改的应用程序状态项的值之前，你应该锁定应用程序状态对象，以便其他用户不能同时修改应用程序状态数据。在完成修改应用程序状态数据后，你应该释放应用程序状态对象，以便其他用户可以访问它。

## How to work with application events

现在你已经知道如何处理应用程序状态数据，你可能会想知道如何初始化应用程序状态项的值。要做到这一点，你首先按照图 8-9 中所述将 `Global.asax` 文件添加到项目中。 （如果你从 ASP.NET Web Site 模板开始项目，此文件已包含在内。）默认情况下，此文件包含五个事件处理程序的方法声明，如本图中的示例所示。然后，你可以向这些事件处理程序中的任何一个添加代码。本图总结了你最有可能用于处理应用程序状态数据的四个事件。

本图中的示例展示了如何初始化和更新一个名为 `HitCount` 的会话状态项，该项用于跟踪为应用程序启动新会话的次数。在此示例中，`Application_Start` 事件处理程序从数据库检索当前命中计数编号，并向应用程序状态对象添加一个名为 `HitCount` 的应用程序状态项。类似地，`Application_End` 事件处理程序将 `HitCount` 项保存到数据库中，以便下次应用程序启动时检索时准确。虽然此处未显示包含用于检索和更新计数的方法的 `HalloweenDB` 类，但你需要知道的是，`GetHitCount` 方法以整数值从数据库检索当前命中计数，而 `UpdateHitCount` 方法将整数值保存到数据库。

`HitCount` 项的更新发生在 `Session_Start` 事件处理程序中，每当新用户会话开始时就会引发该处理程序。此事件处理程序首先锁定应用程序状态对象。然后，它将 `HitCount` 项增加 1 并解锁应用程序状态对象。

## 四个常见的应用程序事件

| Event | Description |
| --- | --- |
| `Application_Start` | 当任何用户请求应用程序的第一个页面时引发此事件。它通常用于初始化应用程序状态项的值。 |
| `Application_End` | 当应用程序即将终止时引发此事件。它可用于将关键应用程序状态项的值写入数据库或文件。 |
| `Session_Start` | 当用户会话开始时引发此事件。它可用于初始化会话状态项、更新应用程序状态项或授权用户访问。 |
| `Session_End` | 当用户会话即将终止时引发此事件。它可用于释放用户占用的资源或将用户注销应用程序。只有在使用进程内模式时才会引发。 |

## 创建应用程序状态中对象的 Global.asax 文件

```
<%@ Application Language="C#" %>
<script runat="server">

    void Application_Start(object sender, EventArgs e)
    {
        // Code that runs on application startup
        Application.Add("HitCount", HalloweenDB.GetHitCount());
    }
    void Application_End(object sender, EventArgs e)
    {
        // Code that runs on application shutdown
        HalloweenDB.UpdateHitCount(Application["HitCount"]);
    }
    void Application_Error(object sender, EventArgs e)
    {
        // Code that runs when an unhandled error occurs
    }
    void Session_Start(object sender, EventArgs e)
    {
        // Code that runs when a new session is started
        Application.Lock();
        int hitCount = Convert.ToInt32(Application["HitCount"]) + 1;
        Application["HitCount"] = hitCount;
        Application.Unlock();
    }
    void Session_End(object sender, EventArgs e)
    {
        // Code that runs when a session ends.
    }
</script>
```

## Description

- 要创建 `Global.asax` 文件，请选择 `Website→Add New Item` 命令，然后选择 `Global Application Class` 模板。
- `Global.asax` 文件为应用程序事件提供事件处理程序。事件处理程序在定义代码声明块的 `Script` 元素内编码。
- 要从 `Global.asax` 文件引用应用程序状态对象，你使用应用程序的 `Application` 属性。

## How to use cookies and URL encoding

本章前面你了解到，视图状态数据存储在发送到浏览器的页面上的隐藏字段中。但视图状态只是你可以使用的基于客户端的状态管理选项之一。另两个是 cookie 和 URL 编码。

## How to create cookies

Cookie 是存储在客户端计算机上的名称/值对。例如，图 8-10 中第一个 cookie 的名称是 `ASP.NET_SessionId`，其值为

```
jsswpu5530hcyx2w3jfa5u55
```

这是 ASP.NET 生成的用于跟踪会话的 cookie 的典型会话 ID。其他 cookie 示例是典型的你自己创建的 cookie。

要创建 cookie，你从 `HttpCookie` 类实例化一个对象。然后，你将其包含在服务器发送回浏览器的 HTTP 响应中，用户浏览器将 cookie 存储在其自己的内存中或客户端机器磁盘上的文本文件中。

存储在浏览器内存中的 cookie 称为会话 cookie，因为它仅存在于该会话期间。当浏览器会话结束时，任何会话 cookie 的内容都会丢失。会话 cookie 是 ASP.NET 用于跟踪会话 ID 的方式。相比之下，持久 cookie 被写入磁盘，因此在浏览器会话结束后仍会被保留。无论是会话 cookie 还是持久 cookie，一旦 cookie 发送到浏览器，它就会随每个 HTTP 请求自动返回到服务器。

除了使用 cookie 作为会话 ID 外，你还可以使用 cookie 保存标识每个用户的信息，以便用户每次访问你的网站时不必每次都输入该信息。你还可以使用 cookie 存储信息，以便个性化为用户显示的网页。
