

在非你自己的机器上进行操作。单击“确定”关闭“高级脚本选项”对话框。

![](img/eadab2ccd79b253c01a3fdff2321202d_806_0.png)

图 19-16

5. 单击“下一步”两次，向导将在你的“文档”文件夹中生成 SQL 脚本（如图 19-16 中的“文件名”框所示）。在记事本中打开该文件，查看其中包含的 SQL 语句。虽然其中大部分内容在你看来可能像天书，但它可以直接用来在兼容的 SQL Server 数据库上重新创建数据库结构和数据。

## 工作原理

数据库的内容可以分为两类：数据库结构和实际数据。当脚本工具运行时，它首先检查数据库的结构，并为在数据库中找到的所有项目创建 SQL CREATE 语句，例如你在前几章中创建的表。然后，它创建 INSERT 语句，以在目标数据库中重新创建所有记录，例如 Reviews、Genres，甚至 users。通过在向导开始时清除“为所有对象编写脚本”复选框，你可以有选择地选择数据库的某些部分，例如，只对几个表编写脚本。

最后，脚本工具会汇总所有 SQL 语句，并将它们保存到一个 .sql 文件中。现在，这个文件就可以在你的主机上运行，以重新创建数据库。

## 重新创建数据库

尽管每个主机在提供对其 SQL Server 的访问权限方面都有自己的规则和程序，但这些规则和程序可以分为三类。

> 注意 有关将网站托管给外部托管方的详细信息，请查看官方 ASP.NET 网站 www.asp.net/learn/hosting 上托管部分的教程。

首先，有些主机不提供对其数据库的远程访问权限，而是要求你提交一个 .sql 文件，以便他们为你执行。在这种情况下，你只需发送文件并等待主机创建数据库，无需做其他任何事情。

第二类主机允许你通过 Web 界面执行 SQL 语句。你通常登录到在线控制面板，然后通过上传文件或将文件内容粘贴到网页的文本区域中，来执行脚本工具创建的 SQL 语句。无论采用哪种方法，最终你都会得到一个可以从应用程序访问的数据库。具体的工作方式因主机而异，请咨询托管服务的帮助或支持系统以获取更多信息。某些提供商基于 Web 的数据库管理工具存在一些已知问题，当你尝试运行生成的 SQL 文件时可能会出错。虽然文件本身在技术上是有效的，但该工具仍可能遇到问题。如果出现这种情况，请联系你的主机以获取解决该问题的帮助。如果你遇到问题，可以尝试的一件事是以不同的格式保存 SQL 文件。默认格式是 Unicode，并非所有提供商都能理解。要更改格式，请在导出数据时为“另存为”选项选择 ANSI 文本，如图 19-16 所示。

最后一类主机允许你通过 Internet 连接到其 SQL Server。这样，你就可以使用 SQL Server Management Studio 等工具，直接从桌面连接到主机上的数据库，并远程执行 SQL 脚本。请参阅第 12 章“使用 SQL 处理数据库数据”部分中的第一个练习，了解如何使用 SSMS 对数据库执行 SQL 文件的更多信息。

在目标服务器上重新创建数据库后，你需要通过更改网站中的连接字符串，重新配置 ASP.NET 应用程序以使用新数据库。为此，你需要修改两个连接字符串：你之前创建的 PlanetWroxConnectionString1 和 PlanetWroxEntities。连接字符串的外观取决于你使用的数据库及其配置。你的托管公司或数据库管理员通常会提供这些信息。有关正确连接字符串的许多示例，请查看 www.connectionstrings.com。以下代码片段提供了一个简单的示例，将你的应用程序重新配置为使用名为 DatabaseServer 的数据库服务器。此示例显示了一个 SQL Server 的连接字符串，要求你使用用户名和密码登录（在你的配置文件中，每个连接字符串应位于单行）：

```
<connectionStrings>
    <add name="PlanetWroxConnectionString1" connectionString="Data Source=DatabaseServer;Initial Catalog=PlanetWrox;User Id=YourUserName; Password=YourPassword;" providerName="System.Data.SqlClient"/>
</connectionStrings>
```

```
<add name="PlanetWroxEntities" connectionString="metadata=res://*/App_Code.PlanetWrox.csdl|res://*/App_Code.PlanetWrox.ssdl|res://*/App_Code.PlanetWrox.msl;provider=System.Data.SqlClient;provider connection string=&quot;Data Source=DatabaseServer;Initial Catalog=PlanetWrox;User Id=YourUserName;Password=YourPassword;MultipleActiveResultSets=True&quot;" providerName="System.Data.EntityClient"/>
</connectionStrings>
```

这将 PlanetWrox 数据库的两个连接字符串都指向了不同的 SQL Server。有关配置 ASP.NET 应用程序和 SQL Server 协同工作的更多信息，请参阅附录 B。

至此，你差不多已经完成了新网站的配置。恭喜！但是，在你放松并开始享受新网站之前，请阅读以下清单，它有助于你保护网站安全并提高其性能。

## 部署清单

本节不是以一些关于部署的一般性提示来结束本章，而是为你提供了一个实用的检查清单，供你在准备将网站投入生产时使用：

- 确保在 Web.config 文件中没有启用调试。这会导致不必要的开销并降低网站性能，因为代码执行速度较慢，而且浏览器无法缓存重要文件。为确保调试已禁用，请打开用于生产环境的 Web.config 文件，并确认 debug 设置为 false：
- 确保你已通过将 Web.config 中 customErrors 元素的 mode 属性设置为 On 或 RemoteOnly，打开了自定义错误。在第一种情况下，每个人都能看到你的自定义错误页面；在第二种情况下，只有 Web 服务器的本地用户才能看到错误详细信息。切勿将 mode 设置为 Off，因为这样做可能导致信息泄露。以下代码片段显示了 customErrors 元素的安全配置：
- 禁用跟踪，或者至少将跟踪信息限制为来自本地机器的用户。Web.config 中的以下 <trace /> 元素会阻止来自 Web 服务器本身以外的机器的用户进行跟踪。此外，它还会阻止跟踪信息出现在页面中：
- 考虑将 machine.config 中 deployment 元素的 retail 属性设置为 true：

```
<compilation debug="false">
```

```
<customErrors mode="On" defaultRedirect="~/Errors/OtherErrors.aspx">
可选的 <error /> 元素在此处
</customErrors>
```

```
<trace mostRecent="true" enabled="true" requestLimit="1000" pageOutput="false" localOnly="true"/>
```

```
<configuration>
<system.web>
```

```
<deployment retail="true"/>
</system.web>
</configuration>
```

此部分用于指示服务器托管你的网站的生产就绪版本，并且对于服务器上的所有站点，它都会将上述三项更改为安全设置：禁用调试和跟踪，并且错误消息仅对本地用户可访问。

要进行此更改，你需要在系统上以管理员身份登录。另外，请务必先备份该文件。因为它充当所有 ASP.NET 网站的根配置文件，你肯定不希望弄乱这个文件。

- 扫描你的网站以查找可能包含敏感信息的重要文件（如 Word 或文本文档），并将它们从发布版本中排除，或考虑将它们移到 App_Data 文件夹中。无法直接访问该文件夹中的文件。但是，你自己的代码仍然可以访问这些文件，就像你在第 9 章中看到的那样。
- 确保你打开了错误日志记录。使用你在上一章中创建的错误日志记录代码，每当发生错误时你都会收到通知，从而能够主动关注服务器，在错误有机会再次发生之前修复它们。
- 如果你在网站中使用主题，请确保从 Web.config 中的 <pages> 元素中移除 styleSheetTheme 属性。Planet Wrox 网站使用主题，但你添加 styleSheetTheme 属性是为了在 Visual Studio 中启用设计时支持。在生产服务器上，你只需要：

```
<pages theme="Monochrome">
...
</pages>
```

这样，页面就不会两次包含同一个样式表。

## 后续内容

既然你已经完成了第一个 ASP.NET 网站，我相信你一定期待着创建下一个网站。Planet Wrox 网站可以作为你将要构建的新网站的基础。你可能不会直接在网站中使用它的任何页面，但希望本书和 Planet Wrox 网站足以激励你独立构建一个新网站。

由于本书面向初学者，我无法就一些重要主题提供大量深入的信息。本书中大多数拥有独立章节的主题，本身都足以写成一本完整的书。例如，CSS、AJAX 和 LINQ 等主题内容非常广泛，Wrox 已经出版了许多相关书籍。既然你已经掌握了这些技术的基础，你可以通过以下 Wrox Professional 系列丛书进一步深入研究：

- Professional CSS: Cascading Style Sheets for Web Design, 3rd Edition (ISBN: 978-0-470-89152-0)
- Professional ASP.NET 2.0 Design: CSS, Themes, and Master Pages (ISBN: 978-0-470-12448-2)
- Professional ASP.NET 4.5 in C# and VB (ISBN: 978-1-118-31182-0)

