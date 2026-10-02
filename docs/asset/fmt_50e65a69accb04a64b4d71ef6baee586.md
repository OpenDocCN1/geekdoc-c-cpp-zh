
# 实体数据模型的映射层

实体数据模型的最后一部分是映射层。该层使用映射语言（`MSL`）映射 `CSDL` 和 `SSDL`。实体数据模型中的三个层可以共享一个通用的类型系统。该系统允许你指定应用程序代码可以理解的类型，然后这些类型将由你所操作的数据库所理解。这三层——概念模型、逻辑模型以及它们之间的映射——以 XML 格式存储在 `.edmx` 文件中。Visual Studio 2012 的优势之处在于，你有一个图形设计器，可以在你的指导下创建这些层以及相应的 `.edmx` 文件。然后可以使用图形设计器对其进行图形显示和编辑，这样你就不需要手动编辑 XML。在使用代码优先开发时，你直接使用 `C#` 或 `VB` 类定义你的模型。你可以使用此模型来生成数据库架构。

# 创建你的第一个实体数据模型

为了演示如何使用 Entity Framework，第一个任务是完成从数据库读取某些数据并使用设计器在你的 ASP.NET 应用程序中展示它的所有步骤。对于此示例，你必须拥有 Visual Studio 2010 或 2012。在此 IDE 中，创建一个名为 `EntityFx` 的空 ASP.NET 应用程序。

注意接下来你必须准备好数据库来进行工作。你可以从 `wrox.com/SQLServer2012` 下载本书使用的 AdventureWorks 数据库版本。要创建添加数据库文件的 `AppData` 文件夹，右键点击项目并选择 **添加 -> ASP.NET 文件夹 -> App_Data**。要添加此数据库，在解决方案管理器中右键点击 `App_Data` 文件夹，并选择 **添加现有项** 选项。

将数据库文件添加到项目后，你需要将数据库升级为 SQL Server LocalDB 数据库。通过选择 Visual Studio 菜单中的 **视图** 来打开服务器管理器。展开 **数据连接** 以查看你刚刚添加的数据库文件。右键点击 `AdventureWorks2012_Data` 连接并选择 **修改连接**。点击按钮显示 **高级属性**。如果 `Data Source` 属性设置为 `(LocalDB)\v11.0` 且 `User Instance` 属性设置为 `False`，图 11-2 显示了具有正确 `Data Source` 和 `User Instance` 设置的高级属性对话框。

点击 **确定** 关闭高级属性对话框，点击 **确定** 关闭修改连接对话框。你将看到一条消息，指示你连接的数据库与当前的 SQL Server 不兼容。图 11-3 显示了此窗口。点击 **是** 升级数据库。

![](img/67a6707ff505c052edb96c0128fb3096_464_0.png)

图 11-2

图 11-3

一旦升级了数据库，你就可以创建实体数据模型了。在 Visual Studio 的解决方案管理器中右键点击你的项目，选择 **添加 -> 新项**。出现新项对话框。在此对话框中，为你正在使用的语言选择 **数据** 选项（位于对话框左侧窗格）。从数据选项可以添加的可用项目包括 **ADO.NET 实体数据模型**，如图 11-4 所示。

对于此示例，将你的实体数据模型命名为 `EDM.edmx`（参考图 11-4）。

# 运行 EDM 向导

点击 **添加** 添加此项并不会立即插入文件，而是启动一个向导。你可以通过两种方式创建实体数据模型。第一个选项是基于预先存在的数据库创建实体数据模型。第二个选项是从空白开始创建实体数据模型。.NET Framework 4-5 让第二个选项变得可以易于处理。当你选择这个第二个选项时，你可以创建实体数据模型，然后使用向导创建该模型的数据库表示。

向导的第一个界面显示这些选项，如图 11-5 所示。

![](img/67a6707ff505c052edb96c0128fb3096_465_0.png)

图 11-4

![](img/67a6707ff505c052edb96c0128fb3096_465_1.png)

图 11-5

对于此示例，选择 **从数据库生成** 选项。在向导中点击 **下一步** 后，下一步是与数据库建立实体连接，如图 11-6 所示。

![](img/67a6707ff505c052edb96c0128fb3096_466_0.png)

图 11-6

此向导允许你从第一个下拉列表中选择你想要操作的数据库。如果你按照之前的指示将其添加到项目，`AdventureWorks2012_Data.mdf` 文件将作为此下拉列表中的选项出现。

在下拉列表中选择此数据库选项时，你将看到实体连接字符串。它看起来像普通的连接字符串：`metadata=res:////EmployeeM.ssdl;res:////EmployeeM.msl;res:////EmployeeM.msl;provider=System.SqlClient;connection string="Data Source=[LocalDB]\mssllocaldb1.0;attachFilename=|DataDirectory|AdventureWorks2012_Data.mdf;integrated security=True;MultipleActiveResultSets=True;App=EntityFramework"`

当你完成此向导页后，点击 **下一步** 来选择你的实体数据模型所需的表、视图和存储过程。

在本示例中，在树视图中展开 **表** 选项，并通过勾选旁边的复选框选择 **Employee (Human Resources)** 表（见图 11-7）。

![](img/67a6707ff505c052edb96c0128fb3096_467_0.png)

图 11-7

注意，向导的这部分允许你定义从代码访问 `AdventureWorks2012_DataModel` 的默认选项。本示例使用了默认选项。此步骤是向导的最后一步。点击 **完成** 按钮，将出现你的实体数据模型的设计界面。

设计界面打开后，可能会收到安全警告，询问你是否想要运行文本模板。设计器使用 `T4` 模板自动生成 `DbContext` 文件以及用于你选择的从数据库生成的每个实体的文件。勾选 **不再显示此消息** 并点击 **确定**。

# 使用 Entity Framework 设计器

Visual Studio 中内置用于处理 Entity Framework 的设计器非常强大，因为它允许你可视化地配置概念层，并控制它如何映射到逻辑层。

如果你之前执行了向导，那么在设计界面上将由一个单一的 `Employee` 对象表示，如图 11-8 所示。

当你突出显示对象的访问修饰符时，Visual Studio 中的 **属性** 窗格中会出现一些基本属性，如图 11-9 所示。

在这里，你可以更改对象的访问修饰符并为该对象提供一些基础文档。Visual Studio 还为你提供了一些处理 Entity framework 的视图。当你创建了 `.edmx` 文件后，系统会为你打开一个视图——**模型浏览器**。

## 创建你的第一个数据模型

![](img/67a6707ff505c052edb96c0128fb3096_468_0.png)

| 属性 | |
| :--- | :--- |
| AdventureWorks2012_DataModelEmployee_Employee 类型 | |
| 代码生成 | False |
| 访问 | Public |
| 图表 | |
| 填充颜色 | 0,122,204 |
| 基类型 | (None) |
| 文档 | |
| 实体集名称 | Employees |
| 名称 | Employee |

图 11-9

另一个重要的视图是 **实体数据模型映射详细** 窗口。你可以通过两种方式进入此视图。你可以从 Visual Studio 菜单选择 **其他窗口** > **实体数据模型映射详细**，或者可以在设计器中右键点击 `Employee` 对象并从提供的菜单中选择 **表映射**。图 11-10 显示了 **实体数据浏览器** 和 **实体数据模型详细** 窗口。

![](img/67a6707ff505c052edb96c0128fb3096_468_1.png)

图 11-10

# 第 11 章 ENTITY FRAMEWORK

现在该对象已就位且 `.edmx` 文件已准备就绪，下一步是构建一个你将实现的简单 ASP.NET Web 表单。

## 使用你的 EDM 构建 ASP.NET Web 表单

现在你已经有了实体数据模型，本节将向你展示如何构建该模型的简单 ASP.NET Web 表单。第一步是向项目添加一个名为 `BasicGrid.aspx` 的新 Web 表单。最后，你的 ASP.NET Web 表单将看起来像列表 11-1 所示的代码（本章节代码中的 `BasicGrid.aspx`）。

### 列表 11-1：一个使用...的简单 ASP.NET Web 表单

```asp
@Page Language="C#" AutoWireup="true" CodeBehind="BasicGrid.cs" Inherits="AspnetFx.BasicGrid" %>
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>My EDM</title>
</head>
<body>
<div id="form1" runat="server">
    <asp:GridView id="GridView1" runat="server"></asp:GridView>
</div>
</body>
</html>
```

这是 Web 表单的 C# 版本。注意页面上只有一个 `GridView`。你将使用此控件来填充来自你创建的实体数据模型的结果。列表 11-2（本章节代码中的 `BasicGrid.aspx` 和 `BasicGrid.cs`）向你展示了 ASP.NET Web 表单的代码后台页。

### 列表 11-2：ASP.NET Web 表单的代码页面

```vb
Partial Class BasicGrid
    Inherits System.Web.Page
    Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs) Handles Me.Load
        Dim adventureWorks2012_DataEntities As New AdventureWorks2012_DataEntities()
        Dim query = From Emp In AdventureWorks2012_DataEntities Select emp
        GridView1.DataSource = query.ToList()
        GridView1.DataBind()
    End Sub
End Class
```

```csharp
using System;
using System.Linq;

namespace AspnetFx
{
    public partial class BasicGrid : System.Web.Page
    {
        protected void Page_Load(object sender, EventArgs args)
        {
            AdventureWorks2012_DataEntities adventureWorks2012_DataEntities =
                new AdventureWorks2012_DataEntities();

            var query = from emp in
                adventureWorks2012_DataEntities.Employees
                select emp;
            GridView1.DataSource = query.ToList();
            GridView1.DataBind();
        }
    }
}
```

如你所见，没有多少代码需要写。运行 Web 表单将产生图 11-11 所示的结果。

| ID | Name | Organization | Level | JobTitle | BirthDate | MaritalStatus | Gender | HireDate | Salary |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 29584724 | adventureworks/k0 | 0 | Chief Executive Officer | 3/2/1963 12:00:00 | S | M | 2/11/2003 12:00:00 | $ |
| 2 | 2457997 | adventureworks/k0 | | Vice President of Engineering | 6/1/1965 12:00:00 | S | M | 3/2/2002 12:00:00 | $ |
| 3 | 5096414 | adventureworks/rob0 | | Engineering Manager | 12/13/1968 12:00:00 | M | M | 12/12/2001 12:00:00 | $ |
| 4 | 11245791 | adventureworks/rob0 | | Senior Tool Designer | 7/13/1969 12:00:00 | S | M | 5/2/2002 12:00:00 | $ |
| 5 | 69526908 | adventureworks/gai0 | | Design Engineer | 10/29/1946 12:00:00 | F | F | 6/2/2002 12:00:00 | $ |
| 6 | 99832069 | adventureworks/jos02 | | Design Engineer | 4/11/1953 12:00:00 | M | M | 2/24/2002 12:00:00 | $ |

图 11-11

## 理解关系

现在对象已就位且 `.edmx` 文件已准备就绪，下一步是构建一个你将实现的简单 ASP.NET Web 表单。

之前的示例很好地展示了一对一映射——一个 `Employee` 对象映射到 `Employee` 表。在本节中，你将查看一对一、一对多以及多对多关系。

为了更详细地展示这一点，你将使用之前示例中的 `Employee` 表。

如果你查看 `Adventure2012_Data.mdf` 数据库文件的详细信息，你会发现有许多不同的表。在本示例使用的实体部分，你可以找到图 11-12 所示的数据库关系。

与这种映射相反，你可以打开在本章稍早创建的 `EmployeeDM.edmx` 文件。在该文件的设计表面上，右键点击并从提供的菜单中选择 **从数据库更新模型**。

会弹出一个更新向导，如图 11-13 所示。

展开 **表** 节点，通过选择每个表旁边的复选框来引用缺失的表——`EmployeeDepartmentHistory`、`Department` 和 `EmployeePayHistory`。从图中你可以看到，与其他类型的员工数据之间存在多对多的关系。

完成此构建后，你还会通过 IntelliSense 发现一个对象映射到每个特定的表，如图 11-14 所示。

![](img/67a6707ff505c052edb96c0128fb3096_472_0.png)

图 11-13

![](img/67a6707ff505c052edb96c0128fb3096_472_1.png)

图 11-14

准备好这些后，你可以像此处演示的那样操作所有对象。对于示例，创建一个仅包含单个 `BulletList` 控件的简单 ASP.NET 表单。从 Web 表单的后台代码中使用列表 11-3 中的代码（本章代码下载中的 `OneToMany.aspx.vb` 和 `OneToMany.aspx.cs`）。

### 列表 11-3：处理一对多映射

#### VB

```vb
Protected Sub Page_Load(ByVal sender As Object, ByVal e As EventArgs)
    Dim adventureWorks2012_DataEntities As New AdventureWorks2012_DataEntities()

    For Each employee In adventureWorks2012_DataEntities
        Dim li As New ListItem()
        li.Text = employee.BusinessEntityID & ""

        For Each pay In employee.EmployeePayHistories
            li.Text &= "Pay Rate: " & pay.Rate & ""
        Next pay

        BulletedList1.Items.Add(li)
    Next employee
End Sub
```

#### C#
