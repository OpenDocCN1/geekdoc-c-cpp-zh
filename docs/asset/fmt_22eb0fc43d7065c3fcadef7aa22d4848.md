
```asp
<@ Page Language="C#" AutoEventWire="true"
CodeBehind="EntityDataSource.aspx.cs" Inherits="AspnetEntityFx.EntityDataSource" %>

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
  <head runat="server">
    <title></title>
  </head>
  <body>
    <form id="form1" runat="server">
      <asp:GridView id="GridView1" runat="server" AllowPaging="true" DataSourceID="EntityDataSource1">
<asp:EntityDataSource ID="EntityDataSource1" runat="server"
  ConnectionString="~AdventureWorks2012_DataEntities"
  DefaultName="AdventureWorks2012_DataEntities"
  EnableDelete="True"
  EnableInsert="False"
  EnableUpdate="True"
  EntityName="Customers">
```

运行此 Web 表单显示图 11 所示的结果。

| CustomerID | PersonID | TerritoryID | AccountName | modifiedDate |
|---|---|---|---|---|
| 1 | 934 | 35ae55b8-b27d-495a-93c7-379af3c8 | | 10/11/2018 11:05:07 AM |
| 2 | 1028 | 35e557a-a9f4-47d3-92c6-c42de241 | | 10/11/2018 11:05:07 AM |
| 3 | 642 | 1307fa41-db21-45f2-99c8-c104b6d56 | | 10/11/2018 11:05:07 AM |
| 4 | 932 | f251f8a-33d4-4551-a633-33333333 | | 10/11/2018 11:05:07 AM |
| 5 | 1026 | 19005990-f15e-4771-b26c-95d0693ea | | 10/11/2018 11:05:07 AM |
| 6 | 644 | 1d02ff88-b6c2-4672-b534-6e647d83 | | 10/11/2018 11:05:07 AM |
| 7 | 930 | 03d9e73e-b916-44e9-b86c-fe6caaed8 | | 10/11/2018 11:05:07 AM |
| 8 | 1024 | 80136ab4-b2f1-4533-927f-f5a3b672 | | 10/11/2018 11:05:07 AM |
| 9 | 620 | 7f51e1e1-c2c3-4b16-8573-95a3b672 | | 10/11/2018 11:05:07 AM |
| 10 | 928 | c6b6f69d-d721-4f8a-8bf2-60ad41d31bd | | 10/11/2018 11:05:07 AM |

```
</form>
</body></html>
```

![](img/67a6707ff505c052edb96c0128fb3096_482_0.png)

图 11

# ENTITY FRAMEWORK CODE FIRST

Code First 在 Entity Framework 的 4.1 版本中引入。Code First 工作流是一种以代码为中心的处理数据和模型的方法。它为数据库 First 优先和使用设计器代码的模型开发工作流提供了替代方案。Code First 采用“约定优于配置”的方法，允许你使用 C# 或 VB 类来定义模型。类可以映射到现有数据库，或用于生成可以创建新数据库的架构。如果需要额外的配置（例如手动映射），可以使用数据注解（data annotations）或 `Fluent API` 来提供详细信息。

Code Migrations（代码迁移）在 Entity Framework 的 4.3 版本中引入。虽然引入了 Migrations，但对 Code First 模型进行更改意味着重新创建数据库。这在应用程序开发期间是可以接受的。但一旦你将应用程序发布到生产环境，每次模型发生变化就删除并重建是不可接受的。就像 Code First 允许你在代码中表示模型一样，Code First Migrations 允许你在代码中表示数据库架构迁移。每当你对要发布的数据库模型进行更改时，就会创建一个迁移。每次迁移都是一个表示自上次迁移以来对模型所做更改的类。因此，你能够直接在项目中维护数据库更改的历史。

# 创建 Code First 模型

向项目中添加一个名为 `CodeFirst.aspx` 的新 Web 表单。在页面上添加 `GridView` 控件。现在你的 ASP.NET 页面将像列表 11-8 所示的代码（显示 C# 代码，本章代码下载中的 `CodeFirst.aspx`）。

# 列表 11-8：使用你的 Code First 模型的基础页面

```cs
<@ Page Language="C#" AutoEventWireup="true" CodeBehind="CodeFirst.aspx.cs"
Inherits="AspNetEntityFX.CodeFirst" %>

<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Code First Model</title>
</head>
<body>
  <form id="form1" runat="server">
    <div>
      <asp:GridView Id="GridView1" runat="server"></asp:GridView>
    </div>
  </form>
</body>
</html>
```

在 ASP.NET 代码后置页面中，你将执行：

1. 创建你的初始模型，该模型将由两个类组成。
2. 然后你将创建一个上下文（context）。上下文是一个表示到数据库会话的类。你使用它来查询和保存数据。为了本示例起见，这些类将简单地添加到同一个文件中 `Page` 类之后。通常，每个这些类都将位于它们自己的文件中。上下文派生自 `System.Data.Entity.DbContext`。
3. 对于模型中的每个类，你将创建一个 `DbSet`。这将告诉 Entity Framework 哪些实体将映射到数据库。
4. 接下来，你向 `Page_Load` 方法添加一些代码，向数据库添加一些数据并显示这些数据。

列表 11-9（本章代码中的 `CodeFirst.aspx.vb` 和 `CodeFirst.aspx.cs`）显示了添加模型类、上下文以及它使用的代码后的后置页面。

# 列表 11-9：CodeFirst ASP.NET 页面的后置页面

## VB

```vb
Imports System.Data.Entity

Public Class CodeFirst
    Inherits System.Web.UI.Page

    Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
        Using context As New TeamContext()
            Dim team = New Team() With {.TeamName = "Team 1"}
            context.Teams.Add(team)
            team = New Team() With {.TeamName = "Team 2"}
            context.Teams.Add(team)
            team = New Team() With {.TeamName = "Team 3"}
            context.Teams.Add(team)
            context.SaveChanges()
            Dim query = From t In context.Teams Select t
            GridView.DataSource = query.ToList()
        End Using
    End Sub
End Class

Public Class Team
    Public Property TeamId() As Integer
    Public Property TeamName() As String
End Class

Public Class Player
    Public Property FirstName() As String
    Public Property LastName() As String
End Class

Public Class TeamContext
    Inherits DbContext
    Public Property Teams As DbSet(Of Team)
    Public Property Players As DbSet(Of Player)
End Class
```

## C#

```csharp
using System;
using System.Collections.Generic;
using System.Data.Entity;
using System.Linq;

namespace AspnetEntityFX
{
    public partial class CodeFirst : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            using (var context = new TeamContext())
            {
                var team = new Team { TeamName = "Team 1" };
                context.Teams.Add(team);
                team = new Team { TeamName = "Team 2" };
                context.Teams.Add(team);
                team = new Team { TeamName = "Team 3" };
                context.Teams.Add(team);
                context.SaveChanges();
            }

            var query = from t in context.Teams select t;
            GridView1.DataSource = query.ToList();
            GridView1.DataBind();
        }
    }
}

public class Team
{
    public int TeamId { get; set; }
    public string TeamName { get; set; }
}

public class Player
{
    public int PlayerId { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}

public class TeamContext : DbContext
{
    public DbSet<Team> Teams { get; set; }
    public DbSet<Player> Players { get; set; }
}
```

这就是让 Entity Framework 根据你的模型创建数据库所需的所有代码。注意，你不需要创建数据库连接，甚至不需要引用连接字符串。这是由于 Code First 的约定优于配置的方法。执行页面将产生如图 11-26 所示的结果。

![](img/67a6707ff505c052edb96c0128fb3096_485_0.png)

图 11-26

为了告诉 Entity Framework 将你的模型类映射到数据库，你为每个模型类创建一个 `DbSet<EntityType>`：

```csharp
public DbSet<Team> Teams { get; set; }
public DbSet<Player> Players { get; set; }
```

为了使用你的模型，你将向数据库添加一些数据。这样做时，你创建一个类的实例，设置其属性并将其添加到 `DbSet`：

```csharp
var team = new Team { TeamName = "Team 1" };
context.Teams.Add(team);
context.SaveChanges();
```

现在你可以使用 LINQ 查询数据：

```csharp
var query = from t in context.Teams select t;
GridView.DataSource = query.ToList();
GridView.DataBind();
```

# C#

```csharp
using System;
using System.Collections.Generic;
using System.Data.Entity;
using System.Linq;
```

```csharp
namespace AspnetEntityFX.CodeFirst
{
    public partial class CodeFirst : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            using (var context = new TeamContext())
            {
                var team = new Team { TeamName = "Team 1" };
                context.Teams.Add(team);
                team = new Team { TeamName = "Team 2" };
                context.Teams.Add(team);
                team = new Team { TeamName = "Team 3" };
                context.Teams.Add(team);
                context.SaveChanges();

                var query = from t in context.Teams select t;
                GridView.DataSource = query.ToList();
                GridView.DataBind();
            }
        }
    }
}
```

```csharp
public class Team
{
    public int TeamId { get; set; }
    public string TeamName { get; set; }
    public virtual List<Player> Players { get; set; }
}
```

```csharp
public class Player
{
    public int PlayerId { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

```csharp
public class TeamContext : DbContext
{
    public DbSet<Team> Teams { get; set; }
    public DbSet<Player> Players { get; set; }
}
```

从 `Team` 到相关 `Player` 实体集合创建了一个关系：

```csharp
public virtual List<Player> Players { get; set; }
```
