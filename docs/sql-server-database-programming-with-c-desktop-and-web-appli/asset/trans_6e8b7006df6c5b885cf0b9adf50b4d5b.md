

# 464

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_492_0.png)

**8.5.3** 完成并添加的新项目都位于该文件夹下。第一个文件是由设计器生成的图 8.54 所示的空白窗口；第二个文件是由关系设计器（Relational Designer）自动生成的，它包含了创建一个派生自 DataContext 类子类 **CSE_DEPTDataContext** 的代码。类中声明了子类 **CSE_DEPTDataContext** 的四个重载构造函数。

要打开关系设计器，在服务器资源管理器（Server Explorer）窗口中双击项目 **CSE_DEPT.dbml**。打开的关系设计器界面如图 8.54 所示。

在创建实体类之前，我们需要连接到示例数据库。要做到这一点，只需点击数据库 **dept-24jpuph/sql/2019.express.cse_DEPT.dbo** 前的箭头，然后展开 **Tables**（表）文件夹以查看所有五个表。

要为每个表创建实体类，需要在服务器资源管理器窗口和空白设计器之间对每个表执行拖放-放置操作。从 **Login**（登录）表开始，将其从服务器资源管理器窗口中拖动并放置到设计视图（Design view）中。通过拖动 **Login** 表设计器，系统将创建实体类并将其添加到 **CSE_DEPT.designer.cs** 文件中。然后，你可以使用此实体类从项目向我们示例数据库 **CSE_DEPT** 中的 Login 表创建并操作数据。

对所有其他表执行类似的拖放-放置操作，完成后的设计器如图 8.55 所示。表与表箭头箭头关联（association），这是 LINQ to SQL 中使用的一个新术语，表示表之间的关系。

现在，我们可以使用这些实体类和 DataContext 通过 LINQ to SQL 技术对示例数据库执行所需的数据操作。

让我们从 **Login** 页面开始，访问示例数据库中的 **Login** 表。

## 8.7.2 通过登录页面执行 LINQ TO SQL 查询登录表

首先，我们需要根据派生上下文类 **CSE_DEPTDataContext** 创建一个字段变量 **cse_dept**。如所述，此对象用于连接到我们的示例数据库。该 DataContext 类提供了多个重载构造函数，但在本应用程序中，我们仅使用简单的一个来简化我们的编码过程。

## 在 ASP.NET 中访问数据

![](img/d59a47501d0a20fc0460a49c469c6fb7_493_0.png)

图 8.54 打开的对象关系设计器。

![](img/d59a47501d0a20fc0460a49c469c6fb7_493_1.png)

图 8.55 完成的设计器。

# 使用 C# 进行 SQL Server 数据库编程

| WebLINQSQL Project | Page_Load(object sender, EventArgs e) |
| :--- | :--- |

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Data;
using System.Data.SqlClient;
using System.Web.UI.Controls;

namespace SQLWebSelect_Project
{
    public class _Default : Page
    {
        WebLINQSQL_Project.CSE_DEPTDataContext cse_dept = new WebLINQSQL_Project.CSE_DEPTDataContext();
        protected void Page_Load(object sender, EventArgs e)
        {
        }
    }
}
```

**图 8.56** 创建字段变量的代码。

打开我们的新项目 **WebLINQSQL Project** 和 **Login.aspx** 页面的代码窗口，将图 8.56 所示的代码输入此代码中，以查看它是如何工作的。

让我们仔细查看这段代码，看看它是如何工作的。

- A. 命名空间 **System.Linq** 自动添加到此代码段中，我们需要使用所有与 LINQ to SQL 相关的数据，而该命名空间包含了所有这些内容。
- B. 使用第一个构造函数创建派生类 **CSE_DEPTDataContext** 的新实例。此实体类生成在我们当前项目下，因此该类必须带有命名空间 **WebLINQSQL_Project** 前缀。否则将遇到编译错误。

这里有一个技巧：此连接对象中没有包含连接字符串。是的，连接字符串在哪里？没有连接字符串我们如何连接到数据库呢？实际上，连接字符串就在那里。在哪里呢？好，让我们现在仔细查看这个问题。

通过双击位于解决方案管理器（Solution Explorer）中的 Web 配置 **Web.config** 来打开它。示例文件如图 8.57 所示。

从此 XML 文件可以找到我们的连接字符串位于 `<ConnectionString>` 标签下，包含了数据源（Data Source）和数据库提供程序（Provider）。在本应用程序中，它是我们数据源的完整名称，包括数据库服务器、数据库名称和身份验证模式。这里使用了 **Windows Authentication Mode**（Windows 身份验证模式）。

当我们创建派生 **DataContext** 类的新实例来连接数据库时，系统会自动从此配置文件加载此连接字符串，即使我们没有明确指示此字符串，它也能连接。**cse_dept** 实例在我们创建它时完成了数据库连接。现在我们可以使用此连接对象对示例数据库执行操作。

## 8.7.2 开发登录和取消按钮的 Click 方法

在 **Login** 页的设计视图中双击 **Login** 按钮打开其 Click 事件方法，并将图 8.58 所示的代码输入此方法。

# 在 ASP.NET 中访问数据

467

![](img/d59a47501d0a20fc0460a49c469c6fb7_495_0.png)

图 8.57. 表单代码示例。

# LINQ2SQL 项目

```csharp
private void cmdLogin_Click(object sender, EventArgs e)
{
    string username = string.Empty;
    string password = string.Empty;
    Selection selfform = new Selection();
    var loginfo = (from log in cse_dept.Tables where log.username == txtUsername.Text && log.password == txtPassword.Text select log).FirstOrDefault();
    if (string.IsNullOrEmpty(txtUsername.Text) || string.IsNullOrEmpty(txtPassword.Text))
    {
        Response.Write("<script>alert('请输入用户名和密码!');</script>");
    }
    else if (loginfo != null)
    {
        Response.Redirect("Selection.aspx");
        cse_dept.Close();
        cse_dept.Dispose();
    }
    else
    {
        Response.Write("<script>alert('登录失败!');</script>");
    }
}
```

图 8.58. 登录按钮的代码。

