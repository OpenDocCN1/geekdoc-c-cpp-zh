
```VB
Public Class NameFunctions

    Private m_FirstName As String
    Private m_LastName As String

    Public Property FirstName() As String
        Get
            Return m_FirstName
        End Get

        Set(ByVal Value As String)
            m_FirstName = Value
        End Set
    End Property

    Public Property LastName() As String
        Get
            Return m_LastName
        End Get

        Set(ByVal Value As String)
            m_LastName = Value
        End Set
    End Property

    Public Property FullName() As String + " " + m_LastName
        Get
            Return m_FirstName + " " + m_LastName
        End Get

    Set(ByVal Value As String)
        m_FirstName = Split(Value, " ")(0)
        m_LastName = Split(Value, " ")(1)
        End Set
    End Property

    Public ReadOnly Property FullNameLength() As Long
        Get
            FullNameLength = Len(Me.FullName)
        End Get
    End Property

End Class
```

```c#
using System;
using System.InteropServices;

namespace NameComponent
{
    [Visible(true)]
    public class NameFunctions
    {
        private string m_FirstName;
        private string m_LastName;

        public string FirstName
        {
            get { return m_FirstName; }
            set { m_FirstName = value; }
        }

        public string LastName
        {
            get { return m_LastName; }
            set { m_LastName = value; }
        }

        public string FullName
        {
            get { return m_FirstName + " " + m_LastName; }
            set
            {
                string[] parts = value.Split(' ');
                m_FirstName = parts[0];
                m_LastName = parts[1];
            }
        }

        public int FullNameLength
        {
            get { return FullName.Length; }
        }
    }
}
```

（注：C# 类的 OCR 文本在不同页面间存在严重碎片化和损坏；我已根据提供的片段和标准的 C# 语法重构了逻辑结构。）

接下来的章节将讨论这两种场景。

# 第 28 章：使用业务对象

## 私有集

私有集意味着将 .NET 组件部署在安装应用程序的每个独立目录下，唯一需要的组件是 .NET DLL 和调用程序。你之前使用 Visual Studio 2008 或 `tlbexp.exe` 创建的交互类型库（Interop Type Library）与引用该 .NET 组件的组件或应用程序静态链接。

你必须完成的额外任务是使用 `regasm.exe` 正确注册 .NET 程序集。这是在 100% 的 .NET 应用中是不需要的额外步骤；它仅用于托管代码引用托管代码的交互性。图 28-15 展示了私有集。

| C:\Program Files\First Application Location\ |  |
| :--- | :--- |
| MyApp.exe (托管代码) | MyDotNet.dll (托管代码) |
| C:\Program Files\Second Application Location\ |  |
| MyApp.exe (托管代码) | MyDotNet.dll (托管代码) |

图 28-15

## 公共集

使用公共集如图 28-16 所示。这种场景涉及将 .NET 组件安装到全局程序集缓存（GAC）。

| C:\Program Files\First Application Location\ | 全局程序集缓存 (GAC) |
| :--- | :--- |
| MyApp.exe (托管代码) | MyDotNet.dll (托管代码) |
| C:\Program Files\Second Application Location\ |  |
| YourApp.exe (托管代码) |  |

图 28-16

与私有集一样，.NET 组件和它的非托管代码是部署的唯一要求——除非需要使用 `regasm.exe` 注册交互程序集。

## 总结

当 .NET 引入时，人们对 ActiveX 控件及其在组件开发未来中的地位最初存在一些担忧。微软立即采取行动，提供了强大的交互（Interop）功能，提供了一种不仅从托管代码到非托管代码，而且从非托管代码到托管代码的通信手段。这种交互性层为许多 Visual Basic 6 开发者提供了开始 .NET 组件开发的方法。

交互性为 .NET 开发者提供了一种方法，可以更新已处于维护阶段的应用程序以及新应用程序，而无需完全重写。

# 第 29 章：ADO.NET Entity Framework

## ADO.NET Entity Framework

如今，访问数据是几乎每个应用程序必须执行的主要任务之一。几乎所有的应用程序都某种方式处理数据，无论这些数据来自内存、数据库、XML 文件还是其他地方。许多开发者发现，从 C# 或 Visual Basic 的强类型面向对象世界到对象是“二等公民”的数据层是困难的。在 ADO.NET Entity Framework 之前，由于许多原因，数据访问会使应用程序开发变得复杂，包括数据库空间和应用程序空间是两个不同的世界。微软一直通过抽象这些困难来简化劳动且容易出错的任务。随着 ADO.NET Entity Framework 的发布，你会发现在数据库和你的应用程序之间导航比任何时候都容易。使用可用的 .NET 编程语言，在代码中使用对象意味着了处理强类型对象的奇妙能力。作为程序员，你可以轻松地在 IDE 中导航，处理底层数据，甚至进行调试。

使用像 ADO.NET Entity Framework（结合 LINQ）的工具，你拥有了一个轻量级的门面（Facade），它为你正在工作的底层数据存储提供了强类型接口。你可以留在编码环境中。

本章提供了 ADO.NET Entity Framework 的概述，以及你如何在你的 ASP.NET 应用程序中使用此框架。需要注意的是，ADO.NET Entity Framework 仅作为 .NET Framework 3.5 SP1 的一部分可用。这意味着除了 Visual Studio 2008 SP1 之外，你还需要安装它。

## 我们能说同一种语言吗？

如所示，构建与数据库通信的应用程序应该是一个更容易的任务。困难之处在于，代码中的对象和数据库中的对象本质上是不同的物种。将对象从数据库层通信到你应用程序堆栈的其他层是增加复杂性的主要原因。

ADO.NET Entity Framework 提供了将对象映射到关系型数据库架构的能力。例如，当你有一个充满了对 `Customer` 对象和 `StoreItem` 对象引用的 `Orders` 表，并且你正在处理关系型数据库架构时，这些实体是通过不同表之间的 `JOIN` 语句创建的。然而，如果你在 C# 或 VB 代码中进行这种构造，那么你正在创建一个 `Order` 对象，它包含一个指向 `Customer` 对象和 `StoreItem` 对象的属性引用。通常情况下，为自己映射这些表示是开发者的工作。

在过去，曾尝试通过引入 `DataSet` 对象来解决这个映射问题。该对象是一个内存中的表表示，包含了多个带有表连接和约束的表。然而，对于人们真正想要开发的纯面向对象代码，`DataSet` 方法通常不被推荐。

当你在数据库内部表示你的数据时，你是通过数据库的关系型架构将其作为一种逻辑模型来表示的。然而，编写你的应用程序是使用概念模型完成的。同时拥有逻辑层和概念层强制要求创建一个映射层。映射层允许你将对象从你在代码中工作的 .NET 类传输到你在数据库中工作的关系型数据库架构。这在图 29-1 中表示。

![](img/eb54f286ad47e89bbf833e2d279e6dd_1370_0.png)

图 29-1

### 层之间的映射

映射层有时被认为是你的数据访问层。在过去的几年里，微软提供了许多数据访问技术，许多第三方公司围绕着让这种映射尽可能简单的概念形成。一些第三方甚至加入，为特殊数据库提供映射或数据访问转换。

微软一直在努力使从应用程序代码到数据库架构的映射变得尽可能简单。ADO.NET Entity Framework 的到位是为了让你能够产出。需要注意的是，在一段时间内，你都需要代码中的对象以及你在关系架构中构建的实体。

EDM 的最后一部分是映射层。该层使用映射规范语言（MSL）映射 CSDL 和 SSDL 实例。

### 概念层和逻辑层

实体模型是你希望在代码中表示数据的抽象概念模型。这通常被构造为 .NET 类，可以像代码中的任何其他对象一样进行操作。你使用概念模式定义语言（CSDL）创建它，它是对象的 XML 定义。.NET Framework 3.5 SP1 和 Visual Studio 2008 SP1 发布的用处在于，你有一个可视化设计器代表你并在你的指导下创建 EDM。

需要注意的是，这些 XML 文件不会与你的代码一起编译，正如我们在本章稍后部分所看到的。

ADO.NET Entity Framework 是微软为 .NET Framework 提供的第一个产品，它提供了实体数据模型（Entity Data Model）及其构造的实现。除了 Entity Framework 的核心部分外，微软还展示了一个 O/R 设计器，用于帮助你创建实体。接下来将演示这些项目。

## 创建你的第一个实体数据模型

为了演示使用 ADO.NET Entity Framework 的示例，第一步是完成从数据库读取数据并在你的 ASP.NET 应用程序中显示的所有步骤。

对于此示例，你需要安装 Visual Studio 2008 SP1。在你的 IDE 中，创建一个名为 `EntityFx` 的新 ASP.NET Web 应用程序。这将创建一个状态化的 ASP.NET 应用程序。

接下来，你需要准备一个数据库进行工作。你可以从 www.codplex.com/MSFTEDProdSamples/Release/ProjectReleases.aspx?Release=4004 下载 AdventureWorks 数据库。你会在该页面找到一个名为 `AdventureWorksDB.msi` 的文件。在解决方案资源器（Solution Explorer）中右键点击 `App_Data` 文件夹，选择添加现有项。

一旦你将数据库文件添加到项目中，就可以创建你的实体数据模型了。在 Visual Studio 的解决方案资源器中右键点击你的项目，选择添加（Add） ➤ 新项（New Item）。在对话框中，从左侧面板中选择你正在使用的语言的 Data 选项。从 Data 选项可以添加的可用项包括 ADO.NET Entity Data Model 项，如图 29–2 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1372_0.png)

图 29-2

对于此示例，你的实体数据模型为 `EmployeeDM.edmx`（参见图 29–2）。

## 运行 EDM 向导

点击确定按钮添加此文件时，实际上不会立即插入文件，而是会启动一个向导。你可以通过两种方式创建实体数据模型：第一个选项是从现有的数据库创建实体数据模型；第二个选项是从空白开始创建实体数据模型。

向导的第一个屏幕显示了这些选项，如图 29-3 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1373_0.png)

对于此示例，选择“从数据库生成”（Generate from database）选项。点击向导中的“下一步”（Next）后，下一步是为数据库建立实体连接字符串。该对话框如图 29-4 所示。

在此向导中，你可以从第一个下拉列表中选择你所使用的数据库。如果你按照之前的指示将它添加到项目，，你将在下拉列表中找到 `AdventureWorks_Data.mdf` 文件作为选项。

当在下拉列表中选择此数据库选项时，你将看到实体连接字符串。这与普通的连接字符串非常相似，

```
metadata-res=**/EmployeeDM.csdl|res://*/EmployeeDM.msl|res://*/EmployeeDM.msl;~CA
provider=System.Data.SqlClient;~CA
provider connection string=*Data Source=SQLEXPRESS;~CA
AttachDbFilename=|Directory\AdventureWorks_Data.mdf;~CA
Integrated Security=True;User Instance='
```

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1374_0.png)

图-24

注意，除了你可能有的普通连接字符串信息（例如提供程序和提供程序连接字符串的属性），你还拥有用于逻辑模型、概念模型以及映射的实体定义。`EmployeeDM.csdl` 文件用于概念模型，`EmployeeDM.ssdi` 用于逻辑模型，而 `EmployeeDM.msi` 用于所需的映射。

该对话框中的最后一个选项类似于你在 ASP.NET 中工作过的大多数提供程序的配置；它允许你将连接字符串保存在项目的 `web.config` 文件中。

当你完成向导的这一页后，点击“下一步”（Next）可以让你选择为实体数据模型所需的表、视图和存储过程。

对于此示例，在树视图中展开 Table（表）选项，通过勾选旁边的复选框选择 Employee (Human Resources) 表（图 29-5）。

注意，向导的这部分允许你定义访问此代码时使用的命名空间。此示例使用了 `AdventureWorks_DataModel` 的默认选项。

这是向导的最后部分。完成选项后，选择“完成”（Finish）按钮。完成向导后，你将看到用于你的实体数据模型的设计表面。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1375_0.png)

图 29-5

## 使用 ADO.NET Entity 设计器

内置在 Visual Studio 2008 SP1 用于 Entity Framework 的 O/R 设计器非常强大，因为它允许你可视化地配置模型。

对于此示例，你的实体数据模型 `EmployeeDM.edmx`（参见图 29–2）。点击确定按钮添加此文件时，实际上不会立即插入文件，而是会启动一个向导。你可以通过两种方式创建实体数据模型：第一个选项是从现有的数据库创建实体数据模型；第二个选项是从空白开始创建实体数据模型。

向导的第一个屏幕显示了这些选项，如图 29-3 所示。对于此示例，选择“从数据库生成”（Generate from database）选项。点击向导中的“下一步”（Next）后，下一步是为数据库建立实体连接字符串。该对话框如图 29-4 所示。

在此向导中，你可以从第一个下拉列表中选择你所使用的数据库。如果你按照之前的指示将它添加到项目中，你将在下拉列表中找到 `AdventureWorks_Data.mdf` 文件作为选项。

当在下拉列表中选择此数据库选项时，你将看到实体连接字符串。这与普通的连接字符串非常相似，

```
metadata-res=**/EmployeeDM.csdl|res://*/EmployeeDM.msl|res://*/EmployeeDM.msl;~CA
provider=System.Data.SqlClient;~CA
provider connection string=*Data Source=SQLEXPRESS;~CA
AttachDbFilename=|Directory\AdventureWorks_Data.mdf;~CA
Integrated Security=True;User Instance='
```
