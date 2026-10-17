
现在，添加代码创建一个新的 `Person`，从文本框填充其字段，并将实例放入进程外会话状态。检索 `Person` 并使用 `ToString()` 方法将其输出到浏览器，见列表 21-5。

> 框架类库中的某些类是不可序列化的。如果你在对象内部使用了此类类型的对象，则这些对象是不可序列化的。例如，如果你在类中包含一个 `DataRow` 字段并将你的对象添加到状态服务，你会收到一条消息提示它是不可序列化的，因为 `DataRow` 包含了不可序列化的对象。

在列表 21-7 中，TextBox 的值被拆分为字符串数组，并将前两个字符串放入 `Person` 实例中。例如，如果你输入 "Christian Wenz"，则 "Christian" 被放入 `Person.firstName`，而 "Wenz" 被放入 `Person.lastName`。当你稍后在列表 21-8 中检索并将其输出到浏览器时，输入的值将会显示。

### 列表 21-7：使用状态服务和基类页面从 Session 设置对象

```vb
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Button1.Click
  Dim names = TextBox.Text.Split(" ") ' 空格创建一个字符
  Dim p As New Person() With {
    .firstName = names(0),
    .lastName = names(1)
  }
  MyPerson = p
End Sub
```

### 列表 21-7（续）

```asp
<asp:Button ID="Button1" runat="server" Text="Store in Session" OnClick="Button1_Click" />
<br />
<asp:HyperLink Id="HyperLink1" runat="server" NavigateUrl="Listing 21-08.aspx">下一页</asp:HyperLink>
</div>
</form>
</body>
</html>
```

### C#

```csharp
<%@ Page Language="C#" Inherits="SmartSessionPage2" %>
<script runat="server">
    protected void Button1_Click(object sender, EventArgs e)
    {
        string[] names = TextBox.Text.Split(' ');
        Person p = new Person()
        {
            firstName = names[0],
            lastName = names[1]
        };
        MyPerson = p;
    }
</script>
```

# 列表 21-8：使用状态和基类从会话检索对象

### VB

```vb
<%@ Page Language="VB" Inherits="SmartSessionPage2" %>
<script runat="server">
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
        Dim p As Person = MyPerson
        Label1.Text = p.ToString()
    End Sub
</script>
```

```html
<!DOCTYPE html>
<html>
<head id="Head1" runat="server">
    <title>未标题的页面</title>
</head>
<body>
<form id="form1" runat="server">
<div>
<asp:Label ID="Label1" runat="server" />
</div>
</form>
</body>
</html>
```

### C#

```csharp
<script runat="server">
  protected void Page_Load(object sender, EventArgs e) {
    Person p = MyPerson;
    Label.Text = p.ToString();
  }
</script>
```

现在，运行带有列表 21-7 的浏览器，输入你的名称，点击按钮启动会话对象，然后通过超链接访问列表 21-8。你将看到结果，如图 21-5 所示。

列表 21-7 和 21-8 中显示的代码和技术说明了会话管理的若干最佳实践：

- 如果你可能使用 InProc 会话状态，请将你的对象标记为**可序列化**（`Serializable`）。
- 更好的是使用本地会话服务器进行所有开发。这将迫使你尽早发现不可序列化的对象，让你了解 `aspnetstate.exe` 的性能和内存使用情况，并允许你在部署时选择任何会话选项。
- 使用具有强类型属性的基类或辅助对象来简化代码。这允许你在整个代码中隐藏会话键。

![](img/6707ff505c05edb9856_0.png)
图 21-5

这些最佳实践适用于所有状态，包括 SQL 状态（稍后介绍）。当使用进程外（out-of-process）会话状态时，存储在该状态中的对象会反复序列化和反序列化以便应用程序运行。移动到序列化内存中的对象可能很大。ASP.NET 4.x 具有压缩存储在进程外状态中的对象的能力。如下代码段所示：

```xml
<sessionState mode="SqlServer"
connectionString="Data Source=observer;Initial Catalog=aspnetstate"
allowCustomDatabase="true"
compressionEnabled="true"/>
```

当通过 `compressionEnabled` 属性启用压缩时，将使用 `System.Compression.GZipStream` 类来压缩对象。默认情况下，`compressionEnabled` 属性设置为 False。通过这种压缩，你会注意到存储状态时使用的内存有显著差异。

# SQL 支持的会话状态

ASP.NET 会话也可以存储在 SQL Server 数据库中。InProc 提供速度，状态服务器提供弹性/速度的平衡，而将会话存储在 SQL Server 中则提供了弹性，可以为大型 Web 农提供服务并在必要时持续 IIS 重启。

SQL 支持的会话状态通过 `aspnet_reg.exe` 配置。此工具添加和删除对许多 ASP.NET 功能的支持，例如缓存依赖项（见第 22 章）和个性化/成员身份（见第 18 和第 19 章），以及会话支持。当你从命令行不带任何选项运行 `aspnet_reg.exe` 时，令人惊讶的是，它会弹 GUI，如图 21-6 所示。此实用程序位于 .NET Framework 的安装目录下，通常位于 `C:\Windows\Microsoft\.NET\Framework\v4.0.30319`。

图 21 对话框中的文本包含了从命令行使用 `-?` 运行 `aspnet_reg` 的指令。你有大量的选项，因此你可能希望将其放在像 `aspnet_reg -? | more` 的形式中。以下是会话状态特定的选项：

## SESSION OPTIONS

- `-ssadd`：添加对 SQLServer 模式状态的支持。
- `-ssremove`：删除对 SQLServer 模式状态的支持。
- `-sstype t|p|c`：会话状态支持的类型：
  - `t`：Temporary。会话状态数据存储在“tempdb”数据库中。管理会话的服务器过程安装在“ASPState”数据库中。如果重启 SQL，数据不会持久。（默认）
  - `p`：持久（persisted）。会话状态数据和存储过程都存储在“ASPState”数据库中。
  - `c`：自定义（custom）。会话状态数据和存储过程都存储在自定义数据库中。必须指定数据库名称。

会话状态支持的三种选项：`t`、`p` 和 `c`。最显著的区别是 `-sstype` 选项在 SQL Server 重启后不会持久会话状态数据，而 `p` 选项可以。使用 `-c` 选项指定自定义数据库并使用 `-d` 指定数据库名称。

命令行示例为你的系统配置 SQL 会话支持，使用本地上的 SQL Server、sa 密码以及 ASPState 数据库中的持久化存储。（当然，你知道不要使用 sa 和弱密码部署你的系统，但这简化了示例。理想情况下，你应该使用 Windows 身份验证，并赋予工作进程身份访问 ASPState 的权限。）

```cmd
aspnet_reg.exe -S localhost -u sa -P wrox -ssadd -sstype p
```

当使用信任连接（Windows 身份验证）时，使用 `-E` 开关：

```cmd
aspnet_reg.exe -S localhost -E -ssadd -sstype p
```

如果你的 SQL Server 安全锁定非常严密，在执行 `aspnet_reg.exe` 后可能会得到 1501 错误，显示“执行 SQL 文件 'InstallSQL.sql' 时发生错误”。SQL 错误代码为 1501，SQLException 消息为：

> 该模块已标记为关闭。启用“Agent XP”以便访问该模块，如果作业不存在，来自 mdb.sp_delete_job 的错误

此信息相当直接，但 `aspnet_reg.exe` 正在试图告诉你，出于安全考虑，它需要的扩展过程被禁用了。你必须显式允许它们。要这样做，请在 SQL Management Studio 中执行以下命令：

```sql
USE master
EXEC sp_configure 'show advanced options', 1
RECONFIGURE WITH OVERIDE
GO
EXEC sp_configure 'Agent XPs', 1
RECONFIGURE WITH OVERIDE
GO
EXEC sp_configure 'show advanced options', 0
RECONFIGURE WITH OVERIDE
GO
```

# 第 21 章 状态管理

![](img/67a6707ff505c052edb96c0128fb3096_859_0.png)

图 21-7 显示了 ASP.NET 跟踪请求详情中看到的 `SessionId`。`SessionId` 出现在你创建的 ASPState 数据库中 `ASPStateTempTables` 表的 `SessionID` 列中。此外，`ASPStateTempApplications` 表还跟踪了可能使用相同数据库管理会话的每个 IIS 应用程序。

如果你想使用数据库来存储会话状态，请使用 `aspnet_reg` 的 `-d` 参数指定数据库名称，并在连接字符串中包含 `allowCustomSqlDatabase=true` 属性以及数据库名称：

```xml
<sessionState allowCustomSqlDatabase="true" mode="SQLServer"
sqlConnectionString="data source=127.0.0.1; database=MyCustomASPStateDatabase;" />
```

用户 ID 和密码可以包含在连接字符串中；或者，如果 ASP.NET 工作进程的身份已配置了访问 SQL Server 的权限，则可以使用 Windows 集成安全验证。

## 使用提供程序扩展会话状态

ASP.NET 会话状态构建在可扩展的基于提供程序的存储模型之上。你可以通过派生 `SessionStateProviderBase` 实现在其他机制中存储会话数据的自定义提供程序。这种扩展性还允许你通过实现 `ISessionManager` 使用自己的算法生成会话 ID。

你首先创建一个实现 `SessionStateProviderBase` 的类。只要会话模块派生自 `SessionStateProviderBase`，会话模块就会调用其任何方法。在应用程序的 web.config 文件中注册你的自定义提供程序如下所示：

```xml
<sessionState mode="Custom" customProvider="WroxProvider">
  <providers>
    <add name="WroxProvider" type="Wrox.WroxStore,Wrox,WSessionSupplier"/>
  </providers>
</sessionState>
```

ASP.NET 初始化 `SessionStateModule`，并且这些方法会在任何自定义实现上被调用：

### 理解 ASP.NET 中的 Session 对象

- **Initialize**：此方法最终继承自 `System.Configuration.ProviderBase`，并在构造函数执行后立即被调用。通过此方法，你可以设置提供程序名称并调用基类的 `Initialize` 实现。
- **SetExpireCallback**：通过此方法，你可以注册任何在会话过期时调用的方法。
- **InitializeRequest**：`SessionStateModule` 为每个请求调用此方法。这是为即将到来的数据做好准备的早期机会。
- **CreateNewStoreData**：通过此方法，你创建一个 `SessionStoreData` 的新实例，`SessionStoreData` 是持有会话项、超时值和任何静态项的数据结构。

当请求会话时，ASP.NET 会调用你的实现来检索它。实现以下方法以检索项：

- **GetItemExclusive**：此方法允许你从所选的存储中获取 `SessionStoreData`。你可能在 XML、Oracle 提供程序中存储了数据。
- **GetItem**：这是你在不使用独占锁的情况下，作为 `GetItemExclusive` 检索数据的机会。这取决于你选择了什么种底层存储。

当需要存储一个项时，会调用以下方法：

- **SetAndReleaseItemExclusive**：在此处，你应该将 `SessionStoreData` 对象保存到你的自定义存储中。

> 注意：ScaleOut Software 以 StateServer 的形式发布了第一个第三方 ASP.NET 状态提供程序。ScaleOut Software 的 StateServer 是运行在 Web 集群中的一种进程外服务，确保会话数据以透明方式存储在集群中的机器之间。你可以访问 scaleout.com 了解更多信息。

## 无 Cookie 会话状态

在之前的示例中，ASP.NET 会话 ID 存储在 cookie 中。某些浏览器不支持 cookie，或者用户可能禁用 cookie。Cookie 是方便的，因为值会在每个请求和响应之间传递。这意味着每个 `HttpRequest` 都包含 cookie 值，而 URL 是每个请求和响应之间传递的唯一内容。如果你在 web.config 文件包含 `cookieless=` 属性，ASP.NET 不会将会话 ID 作为 cookie 发送。相反，会在请求页面之前修改每个 URL 以包含会话 ID：

```xml
<sessionState mode="SQLServer" cookieless="true" sqlConnectionString="data source=127.0.0.1; user=sa;" />
```

注意会话 ID 出现在 URL 中。通过这种更改，Listing 21-1 中使用的服务器端控件（如 `HyperLink`）其属性会自动被修改。如图 21-8 所示。

# 第 21 章 状态管理

![](img/67a6707ff505c052edb96c0128fb3096_859_0.png)
图 21-8

会话 ID 是一个仅包含 ASCII 字符的字符串。当你意识到无 cookie 系统需要将该值放入 URL 时，这是合理的。无 cookie 会话的一个缺点是它们很容易被篡改。由于 cookie 可以被任何人编辑，维护会话的唯一方法是 URL 包含会话 ID。如果调用了如 `/myapp/file.aspx` 的绝对 URL，嵌入 URL 的会话 ID 将丢失。如果你在服务器端生成 URL，使用 `Response.ApplyPathModifier()`。之前的行生成类似：

```csharp
Response.Write(Response.ApplyPathModifier("file.aspx"));
```
