

![](img/c024ccf88e28c30c07dd410d4342288f_806_0.png)

## SQL Server 配置管理器

## 如何安装 SQL Server 2008 Express
- 运行安装程序。当 SQL Server 安装中心对话框显示时，选择 Installation 选项，选择“New installation or add feature to an existing installation”选项以启动 SQL Server 2008 R2 安装向导，并响应随后的对话框。
- 在功能选择步骤中，选择所有可用功能。
- 在实例配置步骤中，使用名称 SQLEXPRESS 创建一个命名实例。
- 在服务器配置步骤中，选择 NT AUTHORITY\SYSTEM 作为 SQL Server 数据库引擎服务的账户名，以便在计算机上运行 SQL Server。
- 在数据库引擎配置步骤中，可以接受 Windows 身份验证模式的默认设置。您也可以单击 Add Current User 按钮，将当前用户添加为 SQL Server 管理员。

## 如何使用 SQL Server Express
- 安装 SQL Server Express 后，每次启动 PC 时它都会自动启动。要启动或停止此服务或更改其启动模式，请启动 SQL Server 配置管理器（开始→所有程序→Microsoft SQL Server 2008 R2→配置工具→SQL Server 配置管理器），在右侧窗格中选择服务器，并使用工具栏中的按钮。
- 安装程序会创建一个名为 SQL Server 的副本，其名称由计算机名称后跟 \SqlExpress 组成。您可以使用此名称来定义与此服务器一起使用的数据库的连接。

## 描述
- 如果您使用的是 Visual Studio 2010，您可以在安装 Visual Studio 的同时安装 SQL Server 2008 Express。
- 如果您使用的是 Visual Web Developer 2008 Express Edition，您可以从 Microsoft 网站免费下载 SQL Server 2008 Express Edition Release 2 的安装文件。然后，您可以运行安装文件来安装 SQL Server Express。

## 如何创建万圣节数据库

如果您想使用随本书下载提供的数据库，您可以毫不费力地做到这一点。首先，您需要按照图 A-1 中所述下载并安装书籍文件。然后，您可以运行位于 C:\Murach\aspnet4_cs\database 目录中的名为 create_database.bat 的批处理文件。此批处理文件运行名为 create_database.sql 的 SQL Server 脚本，该脚本创建万圣节数据库并将其附加到计算机上运行的 SQL Server Express 数据库服务器。

请注意，如果系统上的数据库服务器名称不是计算机名称后加上 SQLEXPRESS，我们提供的批处理文件将无法工作。但您可以轻松更改它使其工作。为此，只需在诸如 NotePad 之类的文本编辑器中打开该文件。当您这样做时，您会看到一条包含此服务器指定的命令：

```
sqlcmd -S localhost\SQLEXPRESS -E /i create_database.sql
```

然后，您只需将此规范更改为您服务器的名称。您还需要对我们提供的其他批处理文件进行此更改。

图 A-6 显示了 create_database.sql 文件的开头。虽然您不需要理解此脚本的所有细节，但您可能希望对它的工作原理有一个大致的了解。

首先，此脚本检查万圣节数据库是否已存在。如果存在，则数据库将被删除。在任何情况下，数据库都会被创建。这使得可以使用此脚本在初始时创建数据库，并在需要时将数据库恢复到原始状态。

创建数据库后，此脚本创建数据库中的每个表，然后向该表插入所需的行。例如，在此图中，您可以看到创建 States 表的 Create Table 语句。此语句后面跟着四个 Insert 语句，将前四行插入表中。类似的语句用于其他每个表。最后，它创建定义表之间关系的外部键约束。

如果您将在 IIS 下运行数据库应用程序，您还需要授予 ASP.NET 对数据库的访问权限。要在 Windows XP 下执行此操作，您可以运行数据库目录中的 grant_access_windows_xp.bat 文件。但首先，您必须修改此批处理文件运行的 grant_access_windows_xp.sql 文件，使其使用您的计算机名称。为此，请在文本编辑器中打开文件，并将每个 [machineName] 的出现替换为您计算机的名称。然后保存并关闭此文件，并运行 grant_access_windows_xp.bat 文件以授予 ASP.NET 对万圣节数据库的访问权限。

您可以使用类似的技术在 Windows 7 和 Windows Vista 下授予 ASP.NET 对数据库的访问权限。具体来说，您运行 grant_access_windows_7_vista.bat 文件，该文件运行 grant_access_windows_7_vista.sql 文件。如果您打开此文件，您会看到它实际上授予对 ASP.NET 4 应用程序池的访问权限。这是如果您在 IIS 下运行 ASP.NET 4 应用程序，您的 ASP.NET 4 应用程序将默认运行的应用程序池。您将在附录 B 中了解有关应用程序池的更多信息。

## 创建万圣节数据库的脚本开头

```
IF DB_ID('Halloween') IS NOT NULL
DROP DATABASE Halloween

CREATE DATABASE Halloween
GO

USE [Halloween]
GO
/****** Object: Table [dbo].[States] Script Date: 01/11/2011 17:06:16
******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[States](
    [StateCode] [char](2) NOT NULL,
    [StateName] [varchar](20) NOT NULL,
CONSTRAINT [PK_States] PRIMARY KEY CLUSTERED
(
    [StateCode] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NO RECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]
GO
SET ANSI_PADDING OFF
GO
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AK', N'Alaska')
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AL', N'Alabama')
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AR', N'Arkansas')
INSERT [dbo].[States] ([StateCode], [StateName]) VALUES (N'AZ', N'Arizona')
.
```

## 描述
- 要创建万圣节数据库，您可以使用 Windows 资源管理器导航到 C:\Murach\aspnet4_cs\database 文件夹并双击 create_database.bat 文件。这将运行创建数据库对象并向每个表插入行的 create_database.sql 文件。
- create_database.sql 文件首先在万圣节数据库已存在时删除它。这样，您就可以在需要时使用它重新创建数据库并恢复原始数据。
- 当您创建万圣节数据库时，两个名为 Halloween.mdf 和 Halloween_log.ldf 的文件将被创建并存储在 SQL Server 实例的默认数据目录中。对于 SQL Server 2008，例如，该目录是 C:\Program files\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA。
- 要在 Windows XP 下授予 ASP.NET 对数据库的访问权限，您修改 grant_access_windows_xp.sql 文件使其使用您的计算机名称，然后运行 grant_access_windows_xp.bat 文件。要在 Windows 7 或 Windows Vista 下执行此操作，您只需运行 grant_access_windows_7_vista.bat 文件。

## 如何使用下载的 Web 应用程序

您可以使用两种技术来运行本书的下载 Web 应用程序。首先，您可以在 Visual Studio 中打开应用程序，然后使用内置开发服务器运行它们。其次，您可以在本地 IIS 服务器下运行它们。图 A-7 描述了这两种技术。

在本地 IIS 服务器下运行应用程序之前，您必须在 IIS 中为应用程序创建一个虚拟目录。虚拟目录是包含指向实际包含网站文件的目录的指针的目录。要创建虚拟目录，您可以使用本图中所示的程序。但首先，如果您使用的是 Windows 7，您应该设置 IIS 在为现有 Visual Studio 应用程序创建虚拟目录时将使用的应用程序池。为此，您可以使用附录 B 中的图 B-4 所示的 IIS 管理控制台。

一旦为 Web 应用程序创建了虚拟目录，您也可以在 Visual Studio 之外运行该应用程序。为此，打开浏览器窗口并指定 //localhost/ 后跟虚拟目录名称和起始页。例如，如果虚拟目录名称为 Ch03Cart 且起始页为 Order.aspx，您可以通过在浏览器地址栏中输入 //localhost/Ch03Cart/Order.aspx 来运行应用程序。

