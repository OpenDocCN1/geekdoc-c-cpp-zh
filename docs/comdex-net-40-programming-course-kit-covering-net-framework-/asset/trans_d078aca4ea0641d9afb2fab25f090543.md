
![](img/9862a98a1a2d3bb14334137965a1ec60_472_0.png)

图 ASP-1.2

在 ASP.NET 4.0 中引入了一项新功能，你可以创建一个空项目，也可以创建一个已具有某种布局和功能的项目。每当你打开一个新网站时，都会出现“新建网站”对话框，如图 ASP-1.3 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_472_1.png)

图 ASP-1.3

这意味着“新建网站”对话框（图 ASP-1.3）现在包含以下两个选项：

- **ASP.NET 网站：** 创建一个新网站，其中包括以下内容：
  - 一个包含成员资格页面、客户端脚本文件和 CSS 文件的文件夹
  - 一个数据文件夹（App_Data）
  - 一个母版页文件（Site.Master）
  - 两个网页：Default.aspx 和 About.aspx
  - 一个全局应用程序文件 Global.asax
  - 一个配置文件 web.config
- **ASP.NET 空网站：** 创建一个新网站，其中仅包含 web.config 文件，不包含其他文件或文件夹。你需要手动添加创建简单网站所需的页面、文件和文件夹。

## 解释 ASP.NET 4.0 提供程序模型

提供程序模型说明了提供程序的位置，提供程序充当数据存储（如 SQL Server）与 ASP.NET 服务（如 ASP.NET 应用程序中的成员资格）之间的桥梁。图 ASP-1.4 显示了 ASP.NET 提供程序模型。

![](img/9862a98a1a2d3bb14334137965a1ec60_473_0.png)

图 ASP-1.4

如图 ASP-1.4 所示，提供程序充当数据源的通信通道。为了进一步说明提供程序的概念，让我们以网上银行网站为例，该网站允许客户访问和修改其账户信息。在这种情况下，银行需要在存储介质（如 Oracle 或 DB2 数据库）中维护每位客户的记录。每当用户尝试通过网站访问信息时，都会选择合适的提供程序，由它检索或更新数据源中的信息。所选提供程序的类型取决于所使用的数据源类型。提供程序的功能类似于从软盘和 CD 等硬件设备中提取数据的设备驱动程序。

根据所提供的服务类型，提供程序可分为两种类型，即成员资格提供程序和角色提供程序。成员资格提供程序存储用户名和密码，角色提供程序存储用户角色。默认情况下，ASP.NET 4.0 使用 AspNetSqlMembershipProvider 提供程序。你可以使用“网站管理工具”或 Microsoft 管理控制台 (MMC) 更改默认提供程序，后者提供称为管理单元的各种管理工具。

表 1.2：列出不同类型的服务提供程序

| 提供程序类型 | 默认提供程序 | 内置提供程序 |
|---|---|---|
| 成员资格 | `System.Web.Security.SqlMembershipProvider` | `System.Web.Security.ActiveDirectoryMembershipProvider`；`System.Web.Security.SqlMembershipProvider` |
| 角色管理 | `System.Web.Security.SqlRoleProvider` | `System.Web.Security.AuthorizationStoreRoleProvider`；`System.Web.Security.SqlRoleProvider`；`System.Web.Security.WindowsTokenRoleProvider` |
| 站点地图 | `System.Web.XmlSiteMapProvider` | `System.Web.XmlSiteMapProvider` |
| 配置文件 | `System.Web.Profile.SqlProfileProvider` | `System.Web.Profile.SqlProfileProvider` |
| 会话状态 | `System.Web.SessionState.InProcSessionStateStore` | `System.Web.SessionState.InProcSessionStateStore`<br>`System.Web.SessionState.OutOfProcSessionStateStore`<br>`System.Web.SessionState.SqlSessionStateStore` |
| Web 事件 | N/A | `System.Web.Management.EventLogWebEventProvider`<br>`System.Web.Management.SimpleMailWebEventProvider`<br>`System.Web.Management.TemplatedMailWebEventProvider`<br>`System.Web.Management.SqlWebEventProvider`<br>`System.Web.Management.TraceWebEventProvider` |
| Web 部件个性化 | `System.Web.UI.WebControls.WebParts.SqlPersonalizationProvider` | `System.Web.UI.WebControls.WebParts.SqlPersonalizationProvider` |
| 受保护的配置 | N/A | `System.Configuration.DPAPIProtectedConfigurationProvider`<br>`System.Configuration.RSAProtectedConfigurationProvider` |

所有提供程序都派生自一个名为 ProviderBase 的公共基类，该类在 `System.Configuration.Provider` 命名空间中定义。

了解提供程序模型后，现在让我们学习编码模型。

## 解释 ASP.NET 4.0 编码模型

ASP.NET 4.0 编码技术是用于在 Web 应用程序中编写代码的方法。ASP.NET 4.0 支持两种不同的编码技术，即单文件页模型和代码隐藏页模型。在单文件编码方法中，开发人员直接在应用程序的 .aspx 页面中编写代码。然而，这种编码模型的一个主要缺点是，你需要在同一个公共文件中编写用于实现 Web 应用程序各种功能的代码和 HTML 代码。这样一来，.aspx 文件中的代码会变得相当复杂且难以管理，尤其是在构建大型应用程序时。为了解决单文件页模型的这一缺点，ASP.NET 4.0 引入了代码隐藏页模型，在该模型中，你需要为每个网页维护单独的代码文件。一个文件存储用某种编程语言（如 VB.NET 和 C#）编写的、用于实现网页功能的代码，另一个文件存储 Web 应用程序的 HTML 标记。以下是 ASP.NET 4.0 中使用的编码模型：

- **单文件页模型：** 指需要将用于实现 Web 应用程序功能的语言脚本代码和 HTML 代码写在同一文件中，但放在不同节中的模型。
- **代码隐藏页模型：** 包含两个独立文件，即 **Default.aspx** 以及 **Default.aspx.cs** 或 **Default.aspx.vb** 之一，分别用于 ASP.NET 呈现标记和实现 Web 应用程序功能的编程逻辑。然后，这两个文件会链接在一起以运行 Web 应用程序。默认情况下，ASP.NET 的所有不同版本——ASP.NET 1.0、ASP.NET 2.0 和 ASP.NET 3.0——都支持此模型。ASP.NET 4.0 中的代码隐藏模型与 ASP.NET 3.5 支持的代码隐藏模型类似。

代码隐藏文件使用分部类而不是主类，并且不继承 .aspx 文件；不过，这两个文件会在编译期间合并在一起，以实现完整的应用程序。

了解 ASP.NET 中的代码模型后，现在让我们学习代码共享。

### 实现代码共享

代码共享是一种机制，通过它可以在 Web 应用程序的不同页面之间共享公共代码。当你希望让具有特定功能的代码可供 Web 应用程序中的所有页面访问时，这尤其有用。以下三种方法用于实现代码共享：

- 使用 Code 目录
- 使用 bin 目录
- 使用全局程序集缓存

### 使用 Code 目录

当你将文件（例如类或 `.wsdl` 文件）添加到 App_Code 文件夹中时，它会被自动检测并编译。编译后，Web 应用程序中的任何页面都可以访问这些文件或类。你需要右键单击“解决方案资源管理器”窗口中的项目名称，然后从上下文菜单中选择“添加 ASP.NET 文件夹”➔“App_Code”选项，以创建 App_Code 文件夹。这会将 App_Code 文件夹添加到“解决方案资源管理器”窗口中。现在，右键单击 App_Code 文件夹并选择“添加新项”选项。将出现“添加新项”对话框，如图 ASP-1.5 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_475_0.png)

图 ASP-1.5 显示了可以添加到 App_Code 文件夹的不同类和文件，以便 Web 应用程序中的所有页面都能访问它们。你可以先选择任何类或文件的图标，然后单击“添加”按钮来添加它。

图 ASP-1.6 显示了“解决方案资源管理器”窗口，其中已将 SQL Server 数据库 Database.mdf 添加到 App_Data 文件夹：

![](img/9862a98a1a2d3bb14334137965a1ec60_475_1.png)

