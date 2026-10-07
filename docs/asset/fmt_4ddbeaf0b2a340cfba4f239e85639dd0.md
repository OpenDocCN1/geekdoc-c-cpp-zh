
```vb
Public ReadOnly Property FullNameLength() As Long
Get
FullLength = Len(Me.FullName)
End Get
```

```vb
End Property
```

```vb
End Class
```

```csharp
using System;
using System.Runtime.InteropServices;
```

```csharp
namespace NameComponent
{
    [ComVisible(true)]
    public class NameFunctions
    {
        private string m_FirstName;
        private string m_LastName;

        public string FirstName
        {
            get
            {
                return m_FirstName;
            }
            set
            {
                m_FirstName=value;
            }
        }

        public string LastName
        {
            get
            {
                return m_LastName;
            }
            set
            {
                m_LastName=value;
            }
        }
    }
```

```csharp
public string FullName
{
    get
        return m_FirstName + " * " + m_LastName;
    }
    set
        m_FirstName=value.Split(' ')[0];
        m_LastName=value.Split(' ')[1];
    }
}
```

```csharp
public long FullNameLength
{
    get
        return this.FullName.Length;
    }
}
```

文件名 `NameFunctions.vb` 和 `NameFunctions.cs`

在创建 .NET 组件后，你就可以创建列表 28-6 所示的消耗 Visual Basic 6 代码。

# 列表 28-6：VB6 代码

```vb
Option Explicit
Sub Main()

Dim o As Object

Set o = CreateObject("NameComponent")

o.FirstName = "Bill"
o.LastName = "Evjen"

MsgBox "Full Name is: " + o.FullName

MsgBox "Length of Full Name is: " + CStr(o.FullNameLength)

Set o = Nothing

End Sub
```

# 1102 | 第 28 章 使用业务对象

## 列表 28-9: 遇到 .NET 错误的 VB6

```vb
Option Explicit

Public Sub Main()

Dim o As Component.DivideFunction

Set o = New Component.DivideFunction

MsgBox "1 divided by 3: * " + CStr(o.divide(1, 3))
MsgBox "1 divided by 0: * " + CStr(o.divide(1, 0))
MsgBox "2000 divided by 3000: * " + CStr(o.divide(2000, 3000))

Set o = Nothing

End Sub
```

列表 28-9 中的 Visual Basic 6 代码没有处理来自 .NET 组件的错误，但可以使用 `On Error`（Visual Basic 6 抛出错误的方法）轻松实现。

与其捕获错误，不如确保 Visual Basic 6 “选项”对话框中的第一个“错误处理”设置为“在类模块中中断”（Break in Class Module）。

当运行应用程序时，第一个以 3 除的示例运行正常；你可以正确看到输出。第二个示例本应该会以除以零错误结束，但它并没有。相反，Visual Basic 6 返回了一个无效的属性值。最后一个示例没有通过 .NET 组件中的自定义错误处理，正如你预期的那样抛出了 Visual Basic 错误。

## 在 COM 应用中部署 .NET 组件

在 COM 应用中部署 .NET 组件与在 .NET 应用中部署 COM 组件类似。这种部署方案存在两种场景：

- 使用私有程序集（private assemblies）

- 使用共享或公共程序集（shared or public assemblies）

后续章节将讨论这两种场景。

## 私有程序集

私有程序集意味着 .NET 组件的部署直接安装在应用程序所在的位置，同一台机器内。所需的组件是 .NET DLL 和调用程序。你之前使用 Studio 2010 或 `tlbexp.exe` 创建的互操作类型库（Interop Type Library）与引用 .NET 组件的组件或应用程序静态链接。

你必须完成的唯一额外任务是使用 `regasm.exe` 正确注册 .NET 程序集。这个额外步骤在 100% 的 .NET 应用程序中都不是需要的；它仅用于非托管代码到托管代码的互操作。使用私有程序集的图 28-15 所示：

![](img/7040c21013b8e6c23c612d6da3599ff8_1161_0.png)

图 28-15

## 公共程序集

图 28-16 展示了公共程序集的使用。这种场景涉及将 .NET 组件安装到全局程序集缓存（GAC）。

| C:\Program Files\First ApplicationLocation\ | 全局程序集缓存 (GAC) |

| :--- | :--- |

| | MyApp.exe (非托管代码) | MyDotNet.dll (托管代码) |

| C:\Program Files\Second ApplicationLocation\ | |

| YourApp.exe (非托管代码) | |

图 28-16

与程序集一样，部署只需要 .NET 组件和消费它的非托管代码——除了需要使用 `regasm.exe` 注册互操作程序集外。

### 总结

当 .NET 引入时，人们对现有的 ActiveX 控制以及它们在微软未来组件开发愿景中的地位产生了一些担忧。微软立即采取行动，提供了稳健且可靠的支持。.NET 互操作功能不仅提供了从 .NET 托管代码到 COM 非托管代码的通信方法，还提供了从 COM 非托管代码到 .NET 托管代码的方法。对于许多 Visual Basic 6 开发者和未来的组件构建者来说，后者是一个意之外但深受欢迎的功能。

这种互操作层使微软能够将 .NET 组件开发推作为一种解决方案，不仅适用于新创建的应用程序，还适用于当前开发中的应用程序以及已经发布并正处于维护阶段的应用程序。

互操作性为 .NET 开发者提供了一种逐步更新应用程序而无需完全重写的方法，并为他们提供了一种无需等待所有支持组件开发完成即可启动新 .NET 项目的方法。

## ADO.NET Entity Framework (实体框架)

### 本章内容

- 理解映射和关系

- 创建实体数据模型 (Entity Data Model)

- 在 EDM 中使用存储过程和 EntityDataSource 

如今，访问数据是几乎每个应用程序必须执行的主要任务之一。许多应用程序以某种方式处理数据，无论这些数据来自内存（内存中数据库）、XML 文件、文本文件或其他。许多开发者发现，从 C# 或 Basic 的强类型面向对象世界到数据层（在那里对象是二等公民而非第一等）是非常困难的。在 ADO.NET Entity Framework 之前，从一个世界到另一个世界的过渡充其量是拙劣的，并且充满了容易出错的操作。数据访问可能会由于多个原因使应用程序开发变得复杂，包括数据库空间和应用程序空间是两个不同的世界。

微软一直尝试通过结合新接口和 IDE 辅助来抽象差异，从而简化程序员那些繁琐且复杂的常见任务。随着 ADO.NET Entity Framework 的早期发布，你会发现在数据库和你的应用程序之间进行导航比以往任何时候都更容易了。

在用其中一种 .NET 编程语言时，在代码中使用对象确实赋予了处理强类型对象的奇妙能力……（注：此处原文存在大量重复句子，译文已按逻辑去重并保留核心意图）。

# 创建你的第一个数据模型 | 1107

最后，实体框架（Entity Framework）由以下部分组成：

- 在应用程序代码中表示的数据库模型

- 你正在使用的数据存储的定义（例如，在 SQL Server 数据库中的数据表示）

- 这两个元素之间的映射

## 概念层与逻辑层

实体数据模型 (EDM) 是根据你想要表示的方式的数据或你代码中的任何其他对象的抽象概念模型。它通常使用 .NET 类构建，你可以像操作其他对象一样对其进行操作。你使用概念架构定义语言 (CSDL) 创建此层，它是你对象的 XML 定义。Visual Studio 2010 的不错之处在于，你有一个视觉化设计器，可以根据你的指示代表你创建 EDM。

请注意，这些 XML 文件不会与你的应用程序一起编译，正如你在本章中看到的。

逻辑层使用存储架构定义语言 (SSDL) 定义，它详细说明了存储在数据库中的关系模式。这包括表、关系及其约束的定义。

## 层与之间的映射

实体数据模型的最后一部分是映射层 (MSL)。该层使用映射规范语言 (MSL) 映射 CSDL 和 SSDL 实例。

由于几个原因，这三层的结合可以协同工作。其是实体数据模型中存在所有层都可以共享的通用类型。该系统允许你指定应用程序将理解的代码类型，并让你正在使用的数据库也能理解这些相同的类型。EDM 还提供了处理继承概念以及复杂对象和与层之间适当映射的能力。

ADO.NET Entity Framework 是微软为 .NET Framework 提供的第一个产品，它提供了实体数据模型及其构造的实现。为了创建实体框架的核心部分，微软还提供了一个 ORM（对象关系）设计器，用于辅助创建你的实体。这些接下来将演示这些项目。

## 创建你的第一个实体数据模型

为了作为使用 ADO.NET Entity Framework 的示例，第一步是完成从数据库读取数据并在你的 ASP.NET 应用程序中显示数据的所有步骤。

对于此示例，你必须拥有 Visual Studio 2008 SP 或 Visual Studio 2010。从此 IDE 中，创建一个名为 `AspEntityFx` 的标准 ASP.NET Web 应用程序。

接下来，你必须找到工作的地方。你可以从 `www.codeplex.com/ProdSamples/Release/ProjectReleases.aspx?ReleaseId-4004` 下载 AdventureWorks 数据库。你会在该页面上找到一个名为 `AdventureWorks.msi` 的文件。要添加此数据库，在解决方案管理器中右键点击 `App_Data` 文件夹并选择添加它。

将数据库添加到项目后，你就可以准备好创建实体数据模型了。在 Visual Studio 的解决方案管理器中右键点击项目并选择“新建项”。出现“添加新建项”对话框。在此对话框中，为你正在使用的语言选择“数据”选项（位于对话框的左侧窗格）。你可以添加到“数据”选项的可用项目包括 ADO.NET 实体数据模型项，如图 29-2 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_1167_0.png)

图 29-2

对于此示例，你的实体数据模型为 `EmployeeDM.edmx`（参考图 29-2）。

## 运行 EDM 向导

点击“添加”按钮添加此不会立即插入文件，而是启动一个向导。你可以通过两种方式创建实体数据模型。第一个选项是基于现有的数据库创建实体数据模型。第二个选项是从空白开始创建实体数据模型。.NET Framework 4 现在真的让这成为你可以轻松操作的内容。当你选择此第二个选项时，你可以创建你的实体数据模型，然后使用向导创建模型的数据库表示。

向导的第一个屏幕显示了这些选项，见图 29-3。

对于此示例，从“数据库”选项进行选择。在向导中点击“下一步”后，下一步是建立到字符串的实体连接，如图 29-4 所示。

![](img/7040c21013b8e6c23c612d6da3599ff8_1167_1.png)

![](img/7040c21013b8e6c23c612d6da3599ff8_1167_2.png)

图 29-3

图 29-4

这允许你从第一个下拉菜单中选择你想要工作的数据库。如果你按照指示将它添加到项目，则下拉菜单中将出现 `AdventureWorks_Data.msi` 文件。

在下拉菜单中选择此数据库时，你将看到实体连接字符串。它看起来可能像一个普通的连接字符串：

```
metadata=res://EmployeeDM.csdl;//EmployeeDM.ssdl;//EmployeeDM.msl;
provider=System.Data.SqlClient;
provider connection="Data Source=SQLServer;Initial Catalog=AdventureWorks_Data;Integrated Security=True;"
```

```html
<head runat="server">
<title>我的 EDM</title>
</head>
<body>
  <form id="form1" runat="server">
<div>
    <asp:GridView Id="GridView1" runat="server">
    </asp:GridView>
</div>
  </form>
</body>
</html>
```

文件名：`BasicGrid.aspx`

这是该页面的 C# 版本。请注意页面上只有一个 GridView 控件。你将使用此控件来填充来自你创建的实体数据模型（Entity Data Model）的查询结果。

要使用实体数据模型，列表 29-2 显示了列表 29-1 所示 ASP.NET 页面的后置代码（code-behind pages）。

# 列表 29-2：ASP.NET 页面的后置代码

```vb
Partial Public Class BasicGrid
Inherits System.Web.UI.Page

Protected Sub Page_Load(ByVal sender As Object,
ByVal e As System.Events.EventArgs Handles Me.Load

Dim adventureWorks_DataEntities As New
AdventureWorks_DataEntities()
```

```vb
Dim query =
From emp In adventureWorks_DataEntities.Employees
Select emp
```

```vb
GridView1.DataSource = query
GridView1.DataBind()
```

```vb
End Sub

End Class
```

```csharp
using System;
using System.Linq;
```

```csharp
namespace AspnetEntityFx
{
    public partial class BasicGrid : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            AdventureWorks_DataEntities adventureWorks_DataEntities =
            new AdventureWorks_DataEntities();

            var query = from emp in
              adventureWorks_DataEntities.Employees
              select emp;
```

# 1112 | 第 29 章 ADO.NET 框架

# 列表 29-2（续）

```csharp
GridView1.DataSource = query;
GridView1.DataBind();
```

文件名：`BasicGrid.aspx.vb` 和 `BasicGrid.aspx`

如你所见，这个页面的代码并不多。运行该页面会产生图 29-9 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_1171_0.png)

图 29-9

要操作你的数据实体模型，需要创建一个模型的一个实例：

```vb
Dim adventureWorks_DataEntities = New AdventureWorks_DataEntities();
```

该实例管理你到数据库的连接，并处理你可能对数据执行的查询。下一行是一个 LINQ 语句：

```vb
Dim query =
From emp in adventureWorks_DataEntities.Employees
Select emp
```
