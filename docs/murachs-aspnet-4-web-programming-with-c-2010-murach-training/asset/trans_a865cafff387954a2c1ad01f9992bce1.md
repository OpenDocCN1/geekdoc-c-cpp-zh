

## 一个计数应用程序，统计用户点击按钮的次数

![](img/c024ccf88e28c30c07dd410d4342288f_308_0.png)

## 计数应用程序的代码

```
int sessionCount;

protected void Page_Load(object sender, EventArgs e)
{
    if (Session["Count"] == null)
        sessionCount = 0;
    else
        sessionCount = Convert.ToInt32(Session["Count"]);
}

protected void btnPost_Click(object sender, EventArgs e)
{
    sessionCount++;
    lblSessionClicks.Text = "You have clicked the button "
        + sessionCount + " times.";
}

protected void Page_PreRender(object sender, EventArgs e)
{
    Session["Count"] = sessionCount;
}
```

## 描述

- 如果会话状态项被两个或多个事件处理程序访问，你通常会编写应用程序使其在 Load 事件处理程序中检索该项的值，并在 PreRender 事件处理程序中将更新后的值保存回会话状态。
- 由于 Load 事件在页面的任何控件事件之前触发，你可以使用其事件处理程序检索会话状态项并将其存储在类级别变量中。然后，该项可供所有其他方法使用。
- 由于 PreRender 事件在所有控件事件处理完毕后触发，你可以使用其事件处理程序更新会话状态项。
- 你只有在该项存储在值类型变量中时才需要显式更新会话状态项。如果它存储在引用类型变量中，则在变量更新时会话状态项会自动更新。

## 存储会话状态数据的选项

默认情况下，ASP.NET 将会话状态数据存储在服务器内存中，并使用 cookie 跟踪用户会话。然而，如图 8-5 所示，ASP.NET 实际上提供了四种存储会话状态数据的选项和两种跟踪会话 ID 的选项。虽然你通常使用默认选项，但在需要时应熟悉这些其他选项。

存储会话状态数据的默认方式是 *in-process mode*。在此模式下，会话状态数据存储在与 ASP.NET 应用程序运行的同一进程中的服务器内存中。这是存储会话状态数据最有效的方式，但它仅适用于托管在单个 Web 服务器上的应用程序。

如果你的应用程序用户太多，单个 Web 服务器无法承受负载，你可以将应用程序部署到两个或多个服务器上。这样做时，你需要将会话状态数据存储在所有服务器都可以访问的位置。会话状态提供了两种执行此操作的方法。

*State Server mode* 将会话状态数据存储在服务器内存中，但不在与应用程序相同的进程中。相反，会话状态由 ASP.NET 状态服务管理，该服务可被托管应用程序的所有服务器访问。这是因为当两个或多个服务器托管应用程序时，每次执行应用程序时都可能由不同的服务器处理。因此，如果会话状态数据存储在应用程序首次执行时处理的服务器上，则当应用程序下次执行时由另一台服务器处理时，该数据将不可用。

使会话状态数据可供两个或多个服务器使用的另一种方法是使用 *SQL Server mode*。在此模式下，会话状态数据存储在 SQL Server 数据库中，而不是服务器内存中。虽然 SQL Server 模式比 in-process 和 State Server 模式慢，但它也是最可靠的。这是因为如果你的 Web 服务器宕机，会话状态数据仍会保存在数据库中。相比之下，如果使用 in-process 或 State Server 模式，服务器宕机时会话状态数据会丢失。

存储会话状态数据的最后一个选项是 *custom mode*。在此模式下，你创建自己的会话状态存储提供程序来保存和检索会话状态数据。你可能会使用此选项，如果你想将会话状态数据保存在数据库中，但你的公司使用 Oracle 或其他数据库而不是 Microsoft SQL Server。

幸运的是，所有四种会话状态模式的编程要求都是相同的。因此，你可以在不更改应用程序代码的情况下将应用程序从一种模式更改为另一种模式。但是，如果你使用自定义模式，你将必须创建会话状态存储提供程序。

## 跟踪会话 ID 的选项

默认情况下，ASP.NET 通过将用户会话的会话 ID 发送到浏览器作为 cookie 来维护会话状态。然后，cookie 会随下一次请求一起返回到服务器，以便服务器可以将浏览器与

会话关联起来。这称为 *cookie-based session tracking*，这是跟踪会话最可靠和最安全的方式。

如果浏览器不支持 cookie，则除非你切换到 *cookieless session tracking*，否则会话状态将无法工作。无 Cookie 会话跟踪通过将会话 ID 添加到用于请求 ASP.NET 页面的 URL 来工作。不幸的是，由于 URL 对用户可见且未加密，使用无 Cookie 会话跟踪会带来安全风险。

因此，理想情况下，当支持 cookie 时应使用基于 cookie 的会话跟踪，当不支持时应使用无 Cookie 会话跟踪。如图 8-6 所示，ASP.NET 允许你这样做。

## 存储会话状态数据的四个选项

- *In-process mode*（默认）将会话状态数据存储在 IIS 服务器内存中，与 ASP.NET 应用程序在同一进程中。这是使用最多的会话状态模式，但仅适用于应用程序使用单个服务器的情况。
- *State Server mode* 将会话状态数据存储在服务器内存中，由名为 ASP.NET 状态服务的单独服务控制。此服务可被其他 IIS 服务器访问，因此当应用程序托管在由多个 IIS 服务器组成的 Web 场上时可以使用。在这种情况下，对应用程序的每个请求都可能由不同的服务器处理，因此会话状态信息必须对所有服务器可用。
- *SQL Server mode* 将会话状态数据存储在 SQL Server 数据库中。与 State Server 模式一样，SQL Server 模式用于需要多个 IIS 服务器的应用程序。虽然此模式比 In-process 模式和 State Server 模式慢，但它也是最可靠的。
- *Custom mode* 允许你编写自己的 *session state store provider* 来读取和写入会话状态数据。

## 跟踪会话 ID 的两个选项

- 默认情况下，ASP.NET 使用 *cookie-based session tracking* 来跟踪用户会话。但是，如果浏览器不支持 cookie，则此方法不起作用。
- 使用 *cookieless session tracking*，会话 ID 被编码为 URL 的一部分。因此，无论浏览器是否支持 cookie，无 Cookie 会话状态都有效。

## 描述

- 所有四种会话状态模式的编程要求都是相同的，因此如果你更改模式，就不需要重新编码应用程序。但是，如果你使用自定义模式，你确实必须创建一个实现会话状态存储提供程序的类。
- 无 Cookie 会话跟踪会带来安全风险，因为会话 ID 对用户可见。它还限制了在 Response.Redirect、Response.RedirectPermanent 和 Server.Transfer 调用中指定 URL 的方式。出于这些原因，大多数开发人员不使用无 Cookie 会话。
- 你可以通过设置应用程序 web.config 文件中会话状态元素的属性来控制会话状态数据的存储方式以及会话 ID 的跟踪方式。有关更多信息，请参阅下一张图。
- Custom mode 是一种高级模式，本书未涵盖。要了解有关如何为自定义模式创建会话状态存储提供程序的更多信息，请参阅帮助文档中的“Implementing a Session-State Store Provider”主题。

## 如何设置会话状态选项

正如你所知，当你创建应用程序时，Visual Studio 会向你的网站添加一个 web.config 文件。然后，你可以按如图 8-6 所示将会话状态选项添加到此文件中。

尽管 web.config 文件是 XML 文件，但即使你不熟悉 XML 语法的细节，也不应难以编辑它。要编辑此文件，只需在解决方案资源管理器中双击它即可在文本编辑器窗口中显示它。然后，如图所示在 system.web 元素内添加 sessionState 元素。在 sessionState 元素内，你可以编码此图中的表中列出的任何属性。在这里显示的示例中，我包含了 mode 属性以指示应使用 in-process 模式；我包含了 cookieless 属性以指示如果支持则应使用 cookie，如果不支持则应使用 URL；我还包含了 timeout 属性以将会话在无活动情况下保持的分钟数增加到 30。

如果你使用 State Server 模式，你需要将 stateConnectionString 属性设置为托管 ASP.NET 状态服务的服务器的名称或 IP 地址和端口号。例如，如果服务器名称为 mma1，则 stateConnectionString 属性将如下所示：

```
stateConnectionString="tcpip=mma1:42424"
```

请注意，端口号始终为 42424。

同样，如果你使用 SQL Server 模式，你需要将 sqlConnectionString 属性设置为包含用于存储会话状态数据的数据库的 SQL Server 实例的连接字符串。例如，如果 SQL Server 实例为 Murach，则该属性可能如下所示：

```
sqlConnectionString="Data Source=Murach;Integrated Security=SSPI"
```

请注意，连接字符串中不包含数据库，这意味着使用名为 ASPState 的默认数据库。如果你想使用不同的数据库来存储会话状态数据，你需要在连接字符串中包含数据库的名称，并且你需要包含 allowCustomSqlDatabase 属性，其值为 True。

如果你使用除 in-process 之外的任何模式，还可以通过将 compressionEnabled 属性设置为 True 来压缩会话状态数据。这是 ASP.NET 4 的新功能，可以使将数据传递到另一台服务器或数据库更有效。

