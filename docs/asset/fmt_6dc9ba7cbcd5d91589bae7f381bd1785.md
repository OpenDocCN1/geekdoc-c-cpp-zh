
如果你使用编程授权检查来运行或显示控件，请确保这些授权检查在底层代码执行期间运行——如果你根据角色检查显示或隐藏用户元素（按钮），请在绑定到这些按钮的任何方法（如 `OnClick()` 事件）中再次检查。

如果资源属于某个用户，在提供服务之前检查当前用户——如果像消息之类的资源是针对特定用户的，那么请检查当前用户是否有权访问该资源。

## 8 安全地访问数据库

在某些时刻，你的 Web 应用程序可能需要使用数据库。一旦你引入数据库，就会引入一系列潜在的漏洞。在本章中，你将学习：

- 简单的查询如何暴露你的数据
- 如何安全地查询数据库
- 如何保护你的 SQL 数据库

> 本章描述的漏洞被称为 SQL 注入。它是攻击者利用向应用程序注入额外语法的一种极其常见的问题。在 2008 年 6 月，数个网站通过 SQL 注入遭受了入侵。你可以在 `http://www.computerworld.com/article/27231/` 了解更多细节。本示例使用了 SQL Express，它是 Visual Studio 的一部分。如果你使用的是 Visual Studio Express，你需要单独下载 SQL Express。你可能发现 SQL Express Management Studio 很有用。你可以从 `https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3B-94B8-5A0F62BF796` 下载。

> 注意 本章从开发者的视角涵盖 SQL，而不是管理员视角。你可能喜欢查看 *Microsoft SQL Server 2008 Administration* (Chris Leiter, Dan Wood, Michael Cierkowski 和 Albert Boetger，2009)，该书对管理和保护 SQL Server 提供了良好介绍。

## 编写错误代码：演示 SQL 注入

此练习的目的是演示 SQL 注入攻击。示例代码代表了不了解 SQL 注入的开发者典型错误。

### 尝试编写具有 SQL 注入漏洞的页面

1. 在 Visual Studio 中创建一个 Web 应用程序。
2. 在解决方案资源管理器窗口中，右键点击 `App_Data` 文件夹并点击“新建”。在新建项目对话框中选择“服务器数据库”，然后点击使用默认文件名 `database.mdf` 的按钮。
3. Visual Studio 将在项目中创建一个新的数据库文件并将其添加到服务器资源管理器窗口。
4. 在服务器资源管理器窗口中，展开并连接数据库。右键点击“表”文件夹并选择“添加表”。

在表定义中，创建名为 `username` 和 `password` 的两个列，数据类型为 `nvarchar(25)`。通过选择列并点击表设计器中的键为 `username` 字段创建主索引，保存表并命名为 `Logins`。你的表看起来像图 8-1 所示。

5. 关闭编辑器返回服务器资源管理器，然后双击新的 `Logins` 表。在新表中，添加一个 `example` 的用户名和 `dropbox` 的密码。你可以通过右键点击服务器资源管理器中的表、选择“显示表数据”，然后输入新行来实现。

## 编写不良代码：演示 SQL 注入

6. 现在，运行解决方案管理器（Solution Explorer）并打开 `default.aspx` 文件。编辑此文件并将默认内容替换为以下内容：

```xml
<% Page Language="C#" AutoEventWireup="true"
CodeFile="default.aspx" Inherits="Default" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/xhtmlml-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head run="server">
<title>SQL Injection Demonstration</title>
</head>
<body
<form id="form" run="server">
<asp:Label Id="Label1" Text="Username: " run="server">
<asp:AssociatedControl Id="Username" run="server"></asp:Label>
<asp:TextBox Id="Username" run="server"></asp:TextBox> br />
<asp:Label Id="Label2" Text="Password: " run="server">
<asp:AssociatedControl Id="Password" run="server"></asp:Label>
<asp:TextBox Id="Password" run="server"></asp:TextBox> br />
<asp:Button Id="submit" run="server" Text="Submit"
onclick="submit_OnClick()" br />
<p>
<strong
<asp:Label Id="Result" run="server"></asp:Label>
</p>
</form>
</body>
</html>
```

7. 将代码文件的内容更改为如下：

```csharp
using System;
using System.Data;
using System.Configuration;
using System.Data.SqlClient;
using System.Web;
using System.Web.UI;
using System.Web.UI.Controls;
```

```csharp
public class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
    }

    protected void submit_OnClick(object sender, EventArgs e)
    {
        string sqlCommand = "select * from logins where username = '" + Username.Text + "' and password = '" + Password.Text + "'";

        using (SqlConnection connection =
            new SqlConnection(ConfigurationManager.ConnectionStrings["database"].ConnectionString)) 
```

```csharp
{
  connection.Open();
  SqlCommand command = new SqlCommand(sqlCommand, connection);

  SqlDataReader reader = command.ExecuteReader();
  if (reader.Read()) {
    Result.Text = "Welcome " + reader["username"];
  } else {
    Result.Text = "Login failed.";
  }

  connection.Close();
}
```

8. 接下来，在你的 `web.config` 文件中，必须为数据库添加一个连接字符串。将 `connectionStrings` 元素更改为：

```xml
<connectionStrings>
  <add name="database"
       connectionString="Server=\SQLServer;AttachDbFilename=|DataDirectory|\database.mdf;
       Database=demoDatabase;
       Trusted_Connection=Yes; />
</connectionStrings>
```

9. 完成后，点击 调试 -> 开始调试（或按 F5）。如果提示页面无法在调试模式下运行，请使用 Visual Studio 调试 `web.config`。
10. 最后，输入用户名和密码示例。点击提交。你应该在提交按钮旁边看到“Welcome example”消息。尝试使用随机数据再次操作查看“Login failed”消息。

> 注意：此时，如果抛出了附加数据库的 SQL 错误，你可能需要在运行代码之前将 Visual Studio 与你的数据库分离。右键点击服务器资源管理器中的数据库，选择“分离数据库”（Detach Database），并重新运行应用程序。你可能还需要编辑 `App_Data` 目录的安全性以允许 SQL Express 读取数据库。要执行此操作，你需要知道 SQL Express 运行所需的用户帐户……（此处由于原文后续存在大量重复和乱码，已根据核心逻辑进行翻译）。

# 尝试使用参数化查询

要对查询进行参数化，你必须更改查询字符串本身以包含参数。

1. 再次打开页面后置代码，对 `submit_OnClick` 方法进行以下高亮更改：

```csharp
protected void submit_OnClick(object sender, EventArgs e)
{
    string sqlCommand = "select * from logins where username = @username and \
    password=@password";

    using (SqlConnection connection =
        new SqlConnection(ConfigurationManager.ConnectionStrings["database"].ConnectionString))
    {
        connection.Open();
        SqlCommand command = new SqlCommand(sqlCommand, connection);

        SqlParameter usernameParameter =
            new SqlParameter("@username", SqlDbType.NVarChar)
            {
                Value = this.Username;
            };
        command.Parameters.Add(usernameParameter);

        SqlParameter passwordParameter =
            new SqlParameter("@password", SqlDbType.NVarChar)
            {
                Value = this.Password;
            };
        command.Parameters.Add(passwordParameter);

        SqlDataReader reader = command.ExecuteReader();

        if (reader.Read())
        {
            Result.Text = "Welcome " + reader["username"];
        }
        else
        {
            Result.Text = "Login failed.";
        }

        connection.Close();
    }
}
```

2. 现在，尝试注入查询并查看是否产生任何副作用——它们没有。参数会为你处理转义任何如单引号之类的特殊字符。

在前面的“尝试一下”练习中进行的更改将 SQL 查询并并更改为使用参数。查询字符串已更改以指定参数，如下所示：

```csharp
string sqlCommand = "select * from logins where username = @username and \
    password=@password";
```

符号 `@` 定义了一个参数。前一个查询中的参数名是 `@username` 和 `@password`。

一旦你有了参数化查询，就必须设置参数的值。这在你从 SQL 查询字符串构建了 `SqlCommand` 命令后完成的，如下：

```csharp
SqlCommand command = new SqlCommand(sqlCommand, connection);

SqlParameter usernameParameter =
    new SqlParameter("@username", SqlDbType.NVarChar, 25);
usernameParameter.Value = this.Username.Text;
command.Parameters.Add(usernameParameter);
```

此代码段创建了一个与查询中的第一个参数 `@username` 匹配的 `SqlParameter` 实例。参数的类型设置为 `NVarChar`，最大长度设置为 25。参数的值根据 `Username` 输入框的 `Text` 属性设置。参数被添加到 `SqlCommand` 实例的 `Parameters` 集合中。这就是所有需要的操作。ADO.NET 会自动处理参数值的清理。

然而，使用任何类型的直接查询（包括参数化查询）都有缺点。数据库的底层架构被暴露，并且 Web 应用程序具有检索的能力。这可能是一个安全问题。通常，你希望对你的数据库引入某种访问控制，防止非管理用户操作原始数据，以防你在其他地方存在漏洞。虽然你可以对列设置权限，但如果用户有能力使用 SQL 查询表，那么该用户就可以看到表中的所有数据。要控制可见的列和存储过程，你必须转向存储过程。

存储过程是在数据库服务器上创建并运行的 SQL 例程，但刻意避免了连接的系统。存储过程可以简单地作为创建、检索、更新和删除（CRUD）操作的封装，也可以包含其自己的逻辑，包括审核数据访问、在检索之前对数据执行计算，或实现其他形式的业务逻辑。

# 尝试使用存储过程

在调用存储过程之前，你必须创建它。虽然 SQL 2005 及更高版本提供了使用 C# 编写存储过程的能力，但这应该被认为是最后的手段——只有当你必须在 SQL 服务器上执行某些 SQL 语言不允许或无法轻易实现的操作时才编写。SQL 语言针对数据操纵进行了优化；而 C# 通常不是。

1. 打开“服务器资源管理器”窗口并连接到在本章开头创建的数据库。右键点击“存储过程”并创建“新建存储过程”。将出现一个新窗口，类似于图 8-2 所示的窗口。

```sql
CREATE PROCEDURE dbo.Storedprocedure
/*
  @parameter1 int = 5,
  @parameter2 datatype OUTPUT
*/
AS
  /* SET NOCOUNT ON **/
  RETURN
```

**图 8-2：** 创建存储过程

从此窗口可以看出，你通过执行 `CREATE PROCEDURE` SQL 命令来创建存储过程。将窗口内容更改为如下：

```sql
CREATE PROCEDURE dbo.GetLogin
(
  @username varchar(25),
  @password varchar(25)
)
AS
  SELECT * FROM logins
  WHERE username = @username AND
  password = @password
```

2. 点击工具栏上的保存按钮，或选择“文件：保存”以将存储过程保存到你的数据库中。一旦完成，它就可以使用了。
3. 使用参数化存储过程就像使用参数化查询，不同之处在于当你为 `Command` 对象创建字符串时，不需要指定参数。打开 `default.aspx` 的代码页并更改 `submit_OnClick`：
