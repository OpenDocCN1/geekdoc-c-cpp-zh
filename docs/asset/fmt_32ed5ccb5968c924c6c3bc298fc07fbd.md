
选中账户后，返回“组或用户名”列表，确保仅勾选了“列文件夹内容”和“读取”。你的对话框最终应与图 19-12 相似。

图 19-12

- 关闭对话框，返回图 19-11 中的“属性”对话框。

- 点击“高级”按钮打开“高级安全设置”对话框。对于 Windows 7 和 Server 2008 R2，点击“更改权限”按钮并勾选“替换子对象权限”。对于 Windows 8 和 Server 2012，你将在“高级安全设置”对话框中找到此复选框。这将强制 Windows 将相同的安全权限应用于所有子文件夹和绑定，替换所有现有设置。点击“确定”并确认已进行更改。最后关闭所有剩余的对话框。

- 回到文件管理器 / Windows 资源管理器，点击 `Release` 文件夹中的 `App_Data`，打开其属性框及其“安全”选项卡，通过添加权限来编辑你在第 4 步中添加的 Web 服务器账户的权限（这将导致某些其他权限也被勾选）。你需要先点击“编辑”按钮将属性对话框变为可编辑模式。图 19-13 显示了完成后的对话框。

点击“确定”关闭对话框。

8. 对 `GigPics` 文件夹重复此步骤，并对 `TempMail` 文件夹也执行此操作。

9. 如果你在带有 SQL Server Express 的机器上使用 IIS，首先需要做的是修改连接字符串。如果你没有安装 SQL Server Express，请参考第 12 章，该章节将向你如何安装 SQL Server Express 以及 SQL Server Management Studio 版。如果你使用的是不同的数据库，或者只安装了 SQL Server Local DB 而不想安装 SQL Server Express，请查看本章后后的“移动到远程服务器”部分并查看附录 B，其中解释了如何配置不同的 SQL Server。

要修改连接字符串，从 `Release` 文件夹打开 `web.config`，并将连接字符串中带有 `.SqlServer` 的两个位置均替换为 `(LocalDB).v11`。这指向命名实例 `SQL Instances=`（在本地机器上调用的 SQL Server，通过点 `.` 标识）。此外，在连接字符串中添加 `UserInstance=True` 以在网站相同的用户账户下运行 SQL Server。你的连接字符串应该如下所示：

```
<connectionStrings>
<add name="PlanetWroxConnectionString1" connectionString="Data Source=\SqlServer;AttachDb=|DataDirectory|\PlanetWrox.sdf;Integrated Security=True;UserInstance=True"
<providerName="System.Data.SqlClient" />
<add name="PlanetWroxConnectionString2" connectionString="Data Source=\.\/App.Code.PlanetWrox.sdl|\/App.Code.PlanetWrox.mdf;providerName=System.Data.SqlClient;attachDbFilename=|DataDirectory|\PlanetWrox.mdf;integrated security=True;User Instance=True;MultipleActiveResultSets=True;App-EntityFramework&quot"
providerName="System.Data.SqlClient" />
</connectionStrings>
```

你还应该在 VS 的转换文件中进行添加，以便在每次发布网站时连接字符串都能正确更新。

10. 要检查网站是否正常工作，打开浏览器并访问 `http://localhost`。你应该能看到 Planet Wrox 网站出现。通过验证一切正常，通过请求菜单中的页面、填写表单、创建新账户、上传图片等操作来浏览网站。如果你在网站页面上收到 404 消息，请从 `Release` 文件夹打开 `Web.config`，将其作为以下代码的直接子节点：

```
<configuration>
```

![](img/9e033e3b9560597824f8b22941d6d8bb_781_0.png)

```
<system.webServer>
  <modules runAllManagedModulesForAllRequests="true"></modules>
</system.webServer>
```

这将没有扩展名的请求（由于 FriendlyUrls 包，这包含了侧边栏的所有页面）映射到 .NET，这样它们就能被正确处理。你也应该将此代码添加到 VS 中的转换文件中，这样下次它添加到你的 .config 文件时，就会自动添加进去。

如果你遇到其他错误，请参考“排排除 Web 服务器错误”部分。

> 注意 如果你仍然无法使其运行，请尝试为 Everyone 配置文件系统。尽管，从安全角度来看，这确实与安全有关。如果你遇到错误，你需要删除的是该账户。

正确且 SQL Server 已配置为允许远程连接。（provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified）——你可能由于多种原因遇到这些错误。虽然这里的错误明确提到了 SQL Server 2008，但你也可以在其他版本的 SQL Server 中遇到此错误。通常，此错误是由无法访问配置的数据库服务器引起的。当你在连接字符串中拼写错了服务器名称，或者服务器只能从本地机器访问而无法通过网络访问时，就会出现此错误。要确保 SQL Server 运行正常，打开管理工具（你在控制面板中使用的工具）中的“服务”部分。查找 SQL Server 并验证 SQL Server 是否已启动。附录 B 详细解释了 SQL 安全性，并为这些问题提供了解决方案。

- 由于无法检索用户的本地应用程序路径数据，无法生成 SQL Server 实例。请确保用户在计算机上拥有本地配置文件。连接将关闭 —— 当你忘记启用“尝试用用”中的“配置你的站点”部分讨论的“加载配置文件”选项时，就会遇到此错误。

**HTTP 错误 500.21** - 内部错误处理器 "PageHandlerFactory-Integration" 模块列表中包含一个错误的模块 "ManagedPipelineHandler"。详细错误信息 —— 当 ASP.NET 未注册时你会遇到此错误，请参考“安装和配置 ASP.NET”标记的节以了解如何修复此问题。

运行时错误说明：服务器上发生应用程序错误。此应用程序当前的自定义错误设置阻止了查看应用程序错误的详细信息。详细要在本地服务器上查看此特定错误消息的详细信息，请在位于当前 Web 应用程序根目录下的 webconfig 配置文件中创建 <customErrors> 标签。此 <customErrors> 标签的 "mode" 属性应设置为 "RemoteOnly"。 —— 当发生运行时错误且 Web 不包含 <customErrors> 元素时，你可能会遇到此错误。当 webconfig 文件包含错误时，你也可能遇到相同的错误；例如，如果你忘记添加某个元素。要修复此类错误，请在 Visual Studio 中打开该文件，它将为你提供有关错误的更多详细信息。

如果你正部署到已安装了 SQL Server 版本的机器，那么你现在已经完成了部署过程。然而，如果你处理的是不同的 SQL Server，唯一需要做的就是确保你的新站点拥有所需的数据。请看下文如何操作。

# 将数据移动到远程服务器

将站点发布到本地机器的 IIS 非常简单。只需将数据复制到新位置，配置 IIS，更改几个安全设置即可。由于站点继续使用你的本地 SQL Server 副本，它将运行良好。

# 第19 章部署你的网站

然而，在现实世界中当你需要将站点移动到外部服务器或主机时，事情并不简单。虽然使用 FTP 程序复制组成站点的文件通常非常简单，但将数据从 SQL Server 数据库复制到主机往往困难。由于大多数主机不支持免费的 Express 或 LocalDB 实例，你不能直接从家中的 `App_Data` 文件夹复制 `.mdf` 文件。相反，这些主机通常提供完整版的 SQL Server，你可以通过基于 Web 的工具或 SQL Server Management Studio 等工具访问它。

将数据库从本地机器传输到远程主机通常有两个步骤：

- 1. 从本地 SQL Server 数据库创建一个 `.sql` 脚本。

- 2. 将此脚本发送到主机并执行它。

在下一节中，你将看到如何将数据库导出为 `.sql` 文件。我不会向你演示如何在主机上重建该文件，因为每个主机的情况不同。相反，我将为你提供一些通用的提示，让你知道要寻找什么。

# 将数据导出到文件

为了方便将数据从本地 SQL Server 数据库传输到你的 Web主机数据库，SQL Server Management Studio 自带了一个工具，可以将数据库结构和数据导出到文件。该文件包含了在远程服务器上重建数据库所需的所有信息。

# 尝试导出数据库

此练习假设你已经下载并安装了 SQL Server Management Studio。如果你还没有，请参考第12章开头获取详细信息。

- 1. 从开始菜单启动 SQL Server Management Studio。你将看到一个类似于图19-14的屏幕。

- 2. 输入服务器名称为 `localdb`，并点击连接。你的数据库已列在 Databases 节点中；如果没有，右键点击 Databases 节点，点击附加（Attach），然后并在 `C:\SQLServer\Site\App_Data` 中浏览你的 `database.mdf` 文件。

- 3. 右键点击数据库并选择任务（Tasks）-> 生成脚本（Generate Scripts）。点击下一步。确保选中了“整个数据库和所有对象”（Entire Database and All Objects），然后点击下一步。出现图19-15所示的对话框。

![](img/9e033e95607824f8b2285_0.png)

图 19-14

- 4. 在此屏幕上，可以在两个输出选项之间选择。第一个允许你创建一个包含必要 SQL 语句的文本文件，第二个允许你通过互联网与共享主机提供商通信。如果你的主机支持此项，它可以在这里提供必要的信息。现在，选择保存到文件（Save to File）。然后点击高级（Advanced）按钮并将脚本类型（Script Types）设置为架构和数据（Schema and Data）。架构的默认值将只编写数据库结构，而不是实际记录。将脚本数据库（Script Database）设置为 False。如果将此设置设置为 True，将允许在 `App_Data` 文件夹中创建数据库，这在你的机器之外的地方可能无法运行。点击确定关闭高级脚本选项对话框。

- 5. 点击下一步，向导会在文件名（File Name）框中指定的位置为你的数据库生成 SQL 脚本。在记事本中打开该文件并查看它包含的 SQL 语句。虽然大部分内容对你来说像乱码，但它是用于在兼容的 SQL Server 上重建数据库结构和数据的。

![](img/9e033e95607824f8b2286_0.png)

图 19-15

## 工作原理

数据库的内容可以分为两类：数据库结构和实际数据。当脚本工具运行时，它首先检查你的数据库结构，并对你在数据库中找到的所有项创建 CREATE 语句，例如你之前创建的表。它会创建 INSERT 语句，以重建数据库中的所有视图、存储过程，甚至用户。通过在向导开始处清除“脚本对象”（Script Objects）复选框，你可以选择性地选择数据库的部分。

最后，脚本工具汇总所有 SQL 语句并将其保存到 `.sql` 文件中。该文件现在可以运行以重建数据库。

# 重建数据库

虽然每个主机在提供 SQL Server 访问方面都有自己的规则和程序，但它们可以分为三类。

> 注意：有关使用外部主机托管站点的详细信息，请查看 ASP.net 网站 www.asp.net/learn/hosting 教程。

首先，某些主机不提供数据库的直接访问，而是要求你提交 `.sql` 文件由他们为你执行。在这种情况下，除了发送文件并等待主机创建数据库外，你不需要做任何其他事情。

第二类主机包含允许通过 Web 界面执行 SQL 语句的主机。你通常登录在线控制面板并执行脚本工具生成的 SQL 语句，可以通过上传文件或将其内容粘贴到网页的文本区域。无论使用哪种方法，你都会得到一个可以从应用程序访问的数据库。具体操作方法每个主机都不同，因此请咨询托管服务的帮助或支持系统获取信息。

最后一类主机允许你通过互联网连接到其 SQL Server。这允许你使用 SQL Server Management Studio 从桌面连接到主机的数据库并远程执行 SQL 语句。

## 部署检查清单 | 75

在目标服务器上重新创建数据库后，你需要通过更改网站中的连接字符串来重新配置 ASP.NET 应用程序以使用新数据库。对于这项工作，你需要修改两个连接字符串：你在前面的章节中创建的 `PlanetWroxConnectionString1` 和 `PlanetWroxEntities`。连接字符串的具体格式取决于你所使用的数据库和配置。你的主机托管公司或数据库管理员通常会提供此类信息。有关正确连接字符串的许多示例，请查看 www.connectionstrings.com。此代码段提供了一个简单的示例，配置你的应用程序使用名为 `DatabaseServer` 的数据库服务器。此示例显示了 SQL Server 的连接字符串，要求你使用用户名和密码登录（在你的配置文件中，连接字符串应该单独成行）：

```xml
<connectionStrings>
<add name="PlanetWroxConnectionString1" connectionString="DataSource=DatabaseServer;Initial Catalog=PlanetWrox;User ID=YourUserName;Password=YourPassword" providerName="System.Data.SqlClient" />
<add name="PlanetWroxEntities" metadata res=":///App_Code.PlanetWrox.ssdlres:///App_Code.PlanetWrox.msdlres://System.Data.SqlClient;provider connectionString="selection=true;Data Source=DatabaseServer;User ID=YourUserName;Password=YourPassword;Initial Catalog=PlanetWrox;MultipleActiveResultSets=True;" providerName="System.Data.EntityClient" />
</connectionStrings>
```

这使 PlanetWrox 数据库的两个连接字符串都指向不同的 SQL Server。有关配置你的 ASP.NET 应用程序和 SQL Server 协同运行的信息，请参阅附录 B。不要忘记在 Visual Studio 的部署配置文件中添加相同的代码，以便下次发布时，目标 `web.config` 具有正确的设置。

在这一阶段，你已经基本完成了新创建网站的配置。恭喜你！然而，在你放松并开始享受你的新网站之前，请阅读以下检查清单，它将帮助你保护网站并提高其性能。

## 部署检查清单

本节并不是用通用的部署技巧来结束本章，而是为你在准备好将网站投入生产环境时提供了一份实用的检查列表：

- 确保你在 `Web.config` 文件中没有启用调试。这会导致不必要的开销并降低网站的性能，因为代码执行速度较慢，且重要文件无法被浏览器缓存。要禁用调试，打开你用于生产环境的 `web.config` 文件，并验证 `debug` 设置为 `false`：

`<compilation debug="false">`

如果你使用了书中所述的 `Web.config` 转换，你的目标 `Web.config` 应该已经关闭此设置。

- 确保通过将 `Web.config` 中 `customErrors` 元素的 `mode` 属性设置为 `On` 或 `RemoteOnly` 来启用自定义错误。在第一情况下，所有人都能看到你的自定义错误页面；在第二种情况下，只有访问 Web 服务器的用户可以看到错误详情。永远不要将 `mode` 设置为 `off`，因为这会导致信息泄露。以下代码段显示了 `customErrors` 元素的配置：

```xml
<customErrors mode="On" defaultredirect="/Errors/OtherErrors.aspx">
可选 <error /> / 元素放在此处
</customErrors>
```

- 禁用跟踪，或者至少禁用向来自本地机器的用户显示跟踪信息。`Web.config` 中的 `<trace />` 元素会阻止来自 Web 服务器本身其他机器用户的跟踪。此外，它还会停止跟踪信息出现在页面中：

```xml
<trace traceRecent="true" enabled="true" requestLimit="1000"
pageOutput="false" localOnly="true"/>
```

将 `machine.config` 中 `deployment` 元素的 `retail` 属性考虑设置为 `true`：

```xml
<configuration>
  <system.web>
    <deployment detail="true"/>
  </system.web>
</configuration>
```

此节用于指示服务器托管了网站的生产就绪版本，并且对于服务器上的所有网站，将之前的三个项目全部更改为安全设置：禁用调试和跟踪，并且错误信息仅对本地用户可见。
