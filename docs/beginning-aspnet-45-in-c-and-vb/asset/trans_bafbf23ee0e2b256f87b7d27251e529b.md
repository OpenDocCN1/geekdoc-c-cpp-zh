
-   2. 在出现的窗口中，展开 SQL Server 网络配置，定位你的 SQL Server 实例并单击它以显示可用协议的列表。如果你正在运行 64 位版本的 Windows，你会看到一个额外的节点，其名称后跟 (32 位)。在这种情况下，找到包含 Protocols for SQLEXPRESS 节点的那个。图 B-1 显示了在 32 位机器上名为 SQLEXPRESS 的 SQL Server 实例的列表。
-   3. 在右侧的协议列表中，右键单击 Named Pipes 并在其状态当前设置为 Disabled 时选择 Enable。
-   4. 重复上一步，但现在启用 TCP/IP。
-   5. 重新启动 SQL Server。为此，在 SQL Server 配置管理器中单击 SQL Server 服务（图 B-1 中显示），然后右键单击你的服务器并选择 Restart。如果出现关于安全权限的错误，你可能需要改而重新启动计算机。

![](img/eadab2ccd79b253c01a3fdff2321202d_841_0.png)

图 B-1

SQL Server 现在允许来自远程机器的传入连接。然而，在你实际使用数据库之前，你需要先将它们附加到 SQL Server。这在下一节中描述。

> 注 如果你连接 SQL Server 时遇到问题，请确保 SQL Server 已安装并正在运行。要验证这一点，请打开控制面板，然后打开位于系统和安全类别中的管理工具部分。接下来，打开服务项，然后验证你正在连接的 SQL Server 实例是否正在运行。如果你将 SQL Server Express 安装在本地机器上并使用默认实例名称，则该服务称为 SQL Server (SQLEXPRESS)。

## 将数据库附加到 SQL Server

SQL Server Express 允许你以两种方式处理数据库文件：你可以在连接字符串中使用特殊属性在运行时附加它们，或在开始使用数据库之前使用 Management Studio 等工具将它们附加。

![](img/eadab2ccd79b253c01a3fdff2321202d_843_0.png)

图 B-2

-   9. 你的数据库现在可在 Management Studio 的对象资源管理器中的 Databases 节点下访问。如果你展开 Databases 元素然后查看你的数据库，你应该会看到熟悉的项目，如表，这些你在本书前面 Visual Studio 中的数据库资源管理器中也看到过。图 B-3 显示了已附加的数据库及其表。

![](img/eadab2ccd79b253c01a3fdff2321202d_843_1.png)

此时，只有管理员帐户（Windows 管理员或名为 SA 的内置 SQL Server 管理员帐户）可以访问数据库。要使 Planet Wrox 网站与这两个数据库一起工作，你需要配置 SQL Server 安全性以及你的网站。你将在接下来看到如何操作。

## 将你的应用程序连接到 SQL Server 2012

在以下部分，我将向你展示如何从两种不同但常见的场景连接到 SQL Server：使用 SQL Server 身份验证，以及在 IIS 和 SQL Server 位于同一服务器时使用 Windows 身份验证。对于这两种场景，你将看到如何配置 SQL Server、Planet Wrox 网站，以及如果需要，你的 Windows 帐户。

图 B-3

你在使用托管你网站的外部托管公司时很可能会使用第一种场景。当网络主机提供 SQL Server 时，它们通常使用 SQL Server 身份验证，因此要求你向数据库服务器传递用户名和密码。

第二种场景在你自行托管网站并且同一台机器上同时有 SQL Server 2012 和 IIS 时很有用。

更高级的场景，例如在两台不同的机器上使用 Windows 身份验证与 IIS 和 SQL Server，则超出了本附录的范围。有关配置和保护 SQL Server 的更多信息，请获取 Adam Jorgensen、Steven Wort、Ross LoForte、Brian Knight 于 2012 年出版的 Professional Microsoft SQL Server 2012 Administration（Wrox，ISBN：978-1-1181-0688-4）。

## 场景 1 — 使用 SQL Server 身份验证

从配置角度来看，这可能是最容易配置的场景：你需要做的就是确保你的 SQL Server 安装支持 SQL Server 身份验证，在 SQL Server 中创建一个用户，然后在 Planet Wrox 网站的连接字符串中使用该帐户。为此，请按照以下步骤操作：

-   1. 在 SQL Server Management Studio 中，右键单击图 B-3 中所示对象资源管理器中的服务器名称，选择 Properties，然后切换到 Security 类别。图 B-4 所示的对话框会出现。

![](img/eadab2ccd79b253c01a3fdff2321202d_844_0.png)

图 B-4

-   2. 如果尚未选择，请在屏幕顶部选择 SQL Server and Windows Authentication Mode 项目。在单击 OK 之前，单击屏幕顶部的 Help 项目，阅读更多关于 SQL 和 Windows 身份验证的内容，并确定你是否真的需要 SQL Server 身份验证。Windows 身份验证比 SQL Server 身份验证更安全，因此建议在可能时使用该选项。
-   3. 如果你更改了服务器身份验证，请重新启动 SQL Server。你可以通过在对象资源管理器中右键单击服务器并选择 Restart 来执行此操作。如果出现关于安全权限的错误，你可能需要重新启动计算机。
-   4. 返回 SQL Server Management Studio 的对象资源管理器，展开图 B-3 底部可见的服务器的 Security 节点。确保你选择的是服务器名称下的那个，而不是属于特定数据库的那个。右键单击 Logins 并选择 New Login。
-   5. 输入登录名，然后选择 SQL Server Authentication 选项，并输入密码（两次）。在此及以下示例中，我将使用 PlanetWroxUser 作为用户名，并使用 Pa$$w0rd（用零代替字母 o）作为密码。
-   6. 清除 Enforce Password Expiration 选项。这也会禁用 User Must Change Password at Next Login。你的对话框应最终看起来像图 B-5 中的那样。

![](img/eadab2ccd79b253c01a3fdff2321202d_845_0.png)

图 B-5

如果你想了解此屏幕上各个设置的更多信息，请单击屏幕顶部的 Help 按钮。

-   7. 单击 OK 以创建新帐户。

帐户创建后，下一步是为此新帐户授予对数据库的适当权限：

-   1. 在对象资源管理器中，展开 Databases，然后展开 PlanetWrox 数据库，后跟 Security 节点。最后，右键单击 Users 节点并选择 New User。
-   2. 在 User Type 下拉列表中，选择 SQL User with Login（此选项在 Management Studio 的早期版本中不存在）。在 User Name 文本框中，输入 PlanetWroxUser。
-   3. 在 Login Name 文本框中再次输入 PlanetWroxUser。或者，单击省略号按钮，然后单击 Browse，并从出现的列表中选择用户。
-   4. 在左侧列表中单击 Membership，你会看到一个标记为 Database Role Membership 的框（在 SQL Server Management Studio 的早期版本中，此框位于输入用户名的同一页面）。在此框中，你可以选择可授予新用户的多个角色。这里的规则是：尽可能少地授予用户权限。一个不错的选择是 db_datareader 和 db_datawriter，这允许帐户同时从数据库中的表读取和写入，因此请选中这两个选项，图 B-6 中可见。

![](img/eadab2ccd79b253c01a3fdff2321202d_846_0.png)

图 B-6

> **注** 请查看 SQL Server 的 Books Online 以获取有关各种角色的更多信息。

-   5. 如果你想为数据库对象设置细粒度的安全选项，请单击图 B-6 左侧部分中看到的 Securables 选项。此对话框使你能够确定用户帐户对数据库中对象（如表、视图和存储过程）的权限。对于 Planet Wrox 网站，你无需在此对话框中进行任何更改。
-   6. 最后，单击 OK 以创建 PlanetWroxUser 帐户并将其分配给 db_datareader 和 db_datawriter 角色。
-   7. 你可以关闭 SQL Server Management Studio，因为目前你已完成使用它。

现在 SQL Server 和你的用户帐户已正确配置，最终阶段是配置网站以使用此新用户帐户。

-   1. 从 C:\BegASPNET\Release 文件夹打开已部署的 Planet Wrox 应用程序的 Web.config 文件。
-   2. 按如下方式修改 <connectionStrings> 元素：
-   3. 保存更改，然后启动浏览器并转到 http://localhost 打开站点。一切仍应正常工作，但站点现在不再使用 App_Data 文件夹中的数据库；它改用你在连接字符串中定义的 SQL Server。

如果你在本地主机上浏览站点时出现错误，你可能需要在 Web.config 中关闭自定义错误（出于安全原因，将其设置为 RemoteOnly 而不是 Off）

```
<connectionStrings>
  <add name="PlanetWroxConnectionString1" connectionString="Data Source=ServerName;Initial Catalog=PlanetWroxUser;password=Pa$w0rd" providerName="System.Data.SqlClient" />
  <add name="PlanetWroxEntities" connectionString="metadata=res://*/App_Code.PlanetWrox.csdl|res://*/App_Code.PlanetWrox.ssdl|res://*/App_Code.PlanetWrox.msl;provider=System.Data.SqlClient;provider connection string="Data Source=ServerName;Initial Catalog=PlanetWrox;User ID=PlanetWroxUser;password=Pa$w0rd;MultipleActiveResultSets=True&quot;" providerName="System.Data.EntityClient" />
</connectionStrings>
```

在你的配置文件中，每个连接字符串应位于单行中。不要忘记用有效的服务器名称替换 Data Source 属性中的值 ServerName。根据你的服务器和配置，这可能像 (local) 或 .\SQLExpress 一样简单，以指向本地机器上的 SQL Server，DatabaseServer 以指向网络上名为 DatabaseServer 的服务器，或像 DatabaseServer\SQL2012 这样指向名为 DatabaseServer 的机器上名为 SQL2012 的命名实例。
