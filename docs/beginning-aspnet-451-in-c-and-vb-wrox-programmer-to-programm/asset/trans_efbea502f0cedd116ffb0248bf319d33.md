

# 将您的应用程序连接到 SQL Server 2012

在后续章节，我将向你展示如何在两种不同的常见场景下连接 SQL Server：使用 SQL Server 身份验证，以及当 IIS 和 SQL Server 位于同一服务器时使用 Windows 身份验证。对于这两种场景，你将看到如何配置 SQL Server、Planet Wrox 网站，必要时还有你的 Windows 账户。

当你处理托管站点的外部托管公司时，可能会使用第一种场景。当网络主机提供 SQL Server 时，他们通常使用 SQL Server 身份验证，因此你需要向数据库传递用户名和密码。

第二种场景是你托管网站，并且 SQL Server 2012 和 IIS 都运行在同一台机器上。

更高级的场景（例如在两个不同的机器上配合 IIS 和 SQL Server 使用 Windows 身份验证）出了附录的范围。有关配置 SQL Server 的更多信息，请购买 Adam Jorgensen、Steven Wort、Ross LoForte 和 Brian Knight 编写的《Professional Microsoft SQL Server 2012 Administration》（2012, Wrox, ISBN: 978-1181-0688-4）。

# 场景 1 — 使用 SQL Server 身份验证

从配置的角度来看，这可能是最容易配置的场景：你只需要确保 SQL Server 安装支持 SQL Server 身份验证，在 SQL Server 中创建一个用户，并在 Planet Wrox 网站的连接字符串中使用该账户。要执行此操作，请遵循以下步骤：

- 1. 在 SQL Server Management Studio 中，右键点击图 B-3 所示的对象管理器中的服务器名称，选择“属性”，并切换到“安全”类别。出现如图 B-4 所示的对话框。

![](img/9e033e3b9560597824f8b22941d6d8bb_824_0.png)

图 B-4

- 2. 如果尚未选择，选择服务器顶部的“SQL Server 和 Windows 身份验证”。在点击 OK 之前，点击屏幕顶部的“帮助”，阅读关于 SQL 和 Windows 身份验证的内容，确定你是否真的需要 SQL Server 身份验证。Windows 身份验证比 SQL Server 身份验证更安全，因此建议尽可能使用它。

- 3. 如果你更改了服务器身份验证方式，请重启 SQL Server。你可以通过右键点击对象管理器中的服务器并选择“重启”来实现。如果遇到安全权限相关的错误，你可能需要重启计算机。

- 4. 在 SQL Server Management Studio 的对象管理器中，展开图 B-3 底部的服务器安全节点。确保选择的是服务器下的，而不是属于数据库的项。右键点击“登录”并选择“新建登录”。

- 5. 输入登录名，然后选择“SQL Server 身份验证”选项并输入密码（两次）。在当前及后续示例中，我将使用 `PlanetWroxUser` 作为用户名，使用 `PaSwOrd`（用数字零代替字母 o）作为密码。

- 6. 取消勾选“强制密码过期”。这将禁用“用户下次登录时必须更改密码”。你的对话框应该看起来如图 B-5 所示。

![](img/9e033e3b9560597824f8b22941d6d8bb_825_0.png)

图 B-5

如果你想了解此屏幕上的各个设置，请点击屏幕顶部的“帮助”按钮。

- 7. 点击 OK 创建新账户。

账户创建后，下一步是为此新账户授予数据库的适当权限：

- 1. 在对象管理器上，展开“数据库”，然后是 PlanetWrox 数据库，最后是“安全”节点。最后，右键点击下拉菜单，选择“具有登录名的 SQL 用户”并选择“新建用户”。

- 2. 在“用户类型”下拉列表中选择“具有登录名的 SQL 用户”（此选项在早期版本的 Management Studio 中不存在）。在“用户名”框中，输入 `PlanetWroxUser`。

- 3. 在“登录名”文本框中，再次点击 `PlanetWroxUser`。或者，点击省略号按钮，点击“浏览”，并从出现的列表中选择该用户。

- 4. 点击左侧列表中的“体系”，看到一个标记为“角色身份”的框（在 SQL Server Management Studio 的早期版本中，此框与输入用户名的在同一页）。在此框中，你可以选择多个可以授予新用户的角色的。这里的规则是：尽可能给用户最少的权限。一个很好的选择是 `db_datareader` 和 `db_datwriter`，它们允许账户同时对数据库进行读取和写入，选择如图 B-6 所示的这两个选项。

![](img/9e033e3b9560597824f8b22941d6d8bb_826_0.png)

图 B-6

- 5. 如果你想为数据库设置细粒度的安全选项，点击图 B-6 左侧部分看到的“安全”选项。此对话框允许你确定用户账户对数据库对象（如表、视图和存储过程）的权限。对于 Planet Wrox 网站，不需要在此对话框中进行任何更改。

- 6. 最后，点击 OK 创建 PlanetWrox 用户并将其分配给 `db_datareader` 和 `db_datwriter`。

- 7. 你可以关闭 SQL Server Management Studio 了，因为你已经完成了操作。

现在 SQL Server 和你的用户账户已配置完毕，最后阶段是配置网站使用此新账户。

- 1. 从 C:\ASNET\Release 文件夹打开部署的 Planet Wrox 应用程序的 `web.config` 文件。

- 2. 如下修改 `<connectionStrings>` 元素：

```
<connectionStrings>
<add name="WroxConnectionString" connectionString="Data Source=ServerName;Initial Catalog=PlanetWrox;User ID=PlanetWroxUser;password=PaSwOrd" providerName="System.Data.SqlClient" />
<add name="PlanetWroxEntities" connectionString="Data Source=ServerName;Initial Catalog=PlanetWrox;User ID=PlanetWroxUser;password=PaSwOrd;MultipleActiveResultSets=True;" provider="System.Data.Entity" />
</connectionStrings>
```

在你的配置文件中，每个连接字符串应占单行。不要忘记将 `Data Source` 中的 `ServerName` 值替换为有效的服务器名称。根据你的服务器和配置，这可能简单如 `(local)` 指向本地机器上的 SQL Server，`DatabaseServer` 指向网络上的服务器，或者像 `DatabaseServer\Sql2012`（这是名为 `DatabaseServer` 的机器上安装的名为 `sql2012` 的实例）。

- 3. 保存更改，然后通过浏览器访问网站。一切应该仍正常工作，但网站不再使用 `App_Data` 文件夹中的数据库；而是使用你在连接字符串中定义的 SQL Server。

- 4. 为了确保此连接字符串在网站未来的更新中可用，你还应该将其添加到 Visual Studio 中网站的 `web.config` 中。

如果你在本地访问网站时遇到错误，你可能需要关闭 `web.config` 中的自定义错误（出于安全考虑，将其设置为 `RemoteOnly` 而不是 `off`）以查看实际错误消息。错误的可能原因包括连接字符串中的用户名、密码或服务器名称错误，以及 `PlanetWroxUser` 账户的角色成员配置错误。

# 场景 2 — 在同一机器上配合 IIS 和数据库使用 Windows 身份验证

这是一个常见场景，特别是当你自己控制的本地机器上运行服务器时。服务器（IIS 或内置开发 Web 服务器）和 SQL Server 都在同一台物理机器上。这种场景使得使用 Windows 身份验证变得简单，因为 Web 服务器和 SQL Server 使用相同的 Windows 账户。

要为此场景配置你的服务器，请遵循以下步骤：

- 1. 确定 Web 服务器使用的账户。有关如何操作的详细信息请参考第19 章，你可能需要 `ApplicationPoolIdentity`（称为 `IIS AppPool\NET v4.5 (default)`）。在本节的剩余部分中我将使用 `IIS AppPool\NET v4.5`。

- 2. 接下来，你需要将此窗口映射到 SQL Server 登录。要执行此操作，打开 SQL Server Management Studio 并登录你的 SQL Server 实例。展开服务器的安全节点（而不是单个数据库的），如图 B-3 底部所示。然后右键点击“登录”并选择“新建登录”。

- 3. 打开 PlanetWrox 数据库的服务器节点，右键点击“用户”节点并选择“新建用户”。

- 4. 在“用户类型”下拉列表中选择“具有登录名的 SQL 用户”（此选项在早期版本的 Management Studio 中不存在）。在“用户名”文本框中，选择 `.NET v4.5`。

- 5. 对于“登录名”文本框，点击省略号按钮并点击“浏览”以选择用户名。选择你之前配置的账户（称为 `IIS AppPool\NET 4.5`）并点击 OK。

- 6. 勾选左侧列表，看到一个标记为“数据库角色身份”的框（在 SQL Server Management Studio 的早期版本中，此框与输入用户名的在同一页）。在此框中，你可以选择多个可以授予新用户的角色的。这里的规则是：尽可能给用户最少的权限。

