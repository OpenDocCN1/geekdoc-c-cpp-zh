

由于两种方法最终都会执行相同的操作（它们都能让你连接到 SQL Server），你可能疑惑自己应该使用其中哪一个。

## 在 Windows 身份验证和 SQL Server 身份验证之间进行选择

通常情况下，建议使用 Windows 身份验证。由于你不需要在连接字符串密码，这意味着你的应用程序将更安全一些。你不需要在网络上传输密码，密码也不会存储在应用程序的配置文件中。

然而，SQL Server 身份验证的设置要简单一些。因为你显式地使用用户名和密码，你不需要知道运行应用程序所需的最终用户账户。

在本附录的后续部分，你将同时使用这两种身份验证机制来连接数据库，你可能需要先查看其他内容：管理 SQL Server 的工具。

## 使用 SQL Server Management Studio

你使用 SQL Server Management Studio（SSMS）来管理 SQL 服务器和数据库。它允许你从 SQL Server 挂载和分离数据库；在现有数据库中创建表等新数据库对象；进行选择、创建、编辑等操作。

目前为止，你一直在使用 SQL Server LocalDB，这是一个对开发者友好的版本。除了 LocalDB，Microsoft 还有另一个免费的 SQL Server 版本称为 SQL Server Express。本附录的后续章节将向你展示如何使用这个免费的 SQL Server 版本，它在使用上与商业和生产级数据库非常相似。如果你只安装了 LocalDB，则需要下载并安装 SQL Server Express 以及免费的 SQL Server Management Studio Express。第 12 章中的“安装 SQL Server 2012 Express”节介绍了如何获取 SQL Server 2012 Express 版以及 Management Studio 组件。

如果你已经在使用 SQL Server 的商业版本，你已经拥有了完整版的 SQL Server Management Studio，因为它是与数据库引擎捆绑的。

如果你在连接远程 SQL Server 时遇到困难（例如，SQL Server 实例不在你运行 Management Studio 的同一台物理服务器上），你可能需要先为该 SQL Server 启用远程连接。将讨论这一点。

## 在 SQL Server 中启用远程连接

在处理 SQL Server 时，你可能会收到一个错误，显示未找到服务器、无法访问或远程连接可能未正确配置。

虽然在数据库服务器宕时可能会遇到此错误，当 SQL Server 未配置远程连接时，你也会遇到此错误。在默认安装中，SQL Server 只允许本地应用程序连接并自动阻止远程连接。要解决此问题并授予远程访问，请遵循以下步骤：

-1. 从开始菜单或搜索中打开“SQL Server 配置管理器”。根据你使用的 SQL Server 版本，此项可能位于“Microsoft SQL Server 2012/配置工具”子菜单下。
 2. 在出现的窗口中，展开“SQL Server 协议”选项以显示可用协议列表（在你的机器上，命名实例 SQLPRESS 可能会有所不同）。如果你运行的是 64 位的 Windows，你将看到一个同名的额外节点，后面带有 (32-bit)。在这种情况下，找到包含 SQLPRESS 协议节点的的节点。图 B-1 显示了 64 位机器上 SQL Server 实例 SQLPRESS 的列表。

![](img/9e033e3b9560597824f8b22941d6d8bb_821_0.png)

图 B-1

-3. 在右侧的协议列表中，右键点击“命名管道 (Named Pipes)”，如果当前状态设置为“已禁用”，则选择“启用”。点击消息框，该框解释了你需要重启 SQL Server 以应用更改。

-4. 重复上述步骤，但现在启用“TCP/IP”。

-5. 重启 SQL Server。要执行操作，点击 SQL Server 配置管理器（如图 B-1 所示）中的“SQL Server 服务”，然后右键点击服务器并选择“重启”。如果你收到有关安全权限的错误，你可能需要重启电脑。

SQL Server 现在允许来自远程机器的传入连接。然而，在实际使用数据库之前，你需要先将其挂载到 SQL Server。这将在下一节中描述。

> 注意 如果在连接 SQL Server 时遇到问题，请确保 SQL Server 已安装并运行。要验证这一点，打开控制面板，然后打开“系统和安全”类别下的“管理工具”。接下来，打开“服务”项，然后验证你正在连接的 SQL Server 实例正在运行。如果你在本地机器上使用默认实例名称安装了 SQL Express，该服务名为 SQL Server (SQLPRESS)。

## 将数据库挂载到 SQL Server

SQL Express 允许你通过两种方式处理数据库文件：你可以在运行时使用连接字符串中的特殊属性来挂载它们，也可以在启动数据库之前使用 Management Studio 等工具来挂载它们。

到目前为止，在数据库相关的章节中，你一直在使用 SQL Server LocalDB 版本使用第一种方案。你使用的 PlanetWrox 连接字符串如下：

```
<add name="PlanetWroxConnectionString"
  connectionString="Data Source=(localdb)\v11.0;
  AttachDb=|DataDirectory|\PlanetWrox.mdf;Trusted_Connection=True;providerName="System.Data.SqlClient" />
```

此连接字符串指向位于网站 App_Data 文件夹中名为 PlanetWrox 的数据库。连接字符串指示 SQL Server 在你使用时将此数据库挂载到 LocalDB。当不再需要时，它会被分离。你可以通过将数据源更改为 .SqlExpress 来针对 SQL Server。

这是本地开发的一个极佳解决方案，因为允许你轻松地创建和移动数据库。然而，对于生产环境，这种选项并不够，你需要先将数据库挂载到 SQL Server。接下来的步骤说明了如何将 PlanetWrox.mdf 挂载到 SQL Server（如果你想使用 Management Studio 执行维护任务）。

-1. 创建一个用于存放数据库的文件夹，例如 C:\Data\SqlServer。
-2. 将 PlanetWrox.mdf 移动到此文件夹。
-3. 为 SQL Server 使用的帐户（默认为 Network Service 帐户）以及你的帐户对该文件夹（C:\Data\SqlServer）修改权限。第 19 章介绍了如何设置这些权限。
-4. 打开 SQL Server Management Studio 并登录你要挂载数据库的 SQL Server 实例。根据安全设置，你可能需要管理员身份运行此过程。对于 Windows 7 或 Server 2008，右键点击 Management Studio 项并选择“以管理员身份运行”。对于 Windows 8 或 Server 2012，右键点击屏幕上的项目并选择“以管理员身份运行”。
-5. 右键点击“数据库”节点并选择“挂载”。
-6. 在随后的对话框中点击“添加”，选择移动到 C:\Data\SqlServer 的 PlanetWrox.mdf 文件。
-7. 点击挂载列的值使其可编辑，并输入 PlanetWrox 作为赋予数据库的新名称。完成后，你的对话框应像图 B-2。

![](img/9e033e3b9560597824f8b22941d6d8bb_823_0.png)

图 B-2

点击 OK 将数据库挂载到 SQL Server。如果你遇到错误，请确保你的帐户（或你所属的用户组）以及 Network Service 帐户对 c:\Data\SqlServer 文件夹以及该文件夹包含的 .mdf 文件具有修改权限。此外，按照第 4 步尝试以管理员身份运行 Management Studio。

你的数据库现在可以在 Management Studio 对象资源器的器的数据库”节点中访问。如果你展开元素并查看你的数据库，你应该看到之前在 Visual Studio 的服务器资源管理器中看到的熟悉的项目，如表。图 B-3 显示了挂载的数据库及其表。

