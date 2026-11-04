
The next screen of the wizard will find your NORTHWIND.mdf database and pre-define the connection settings and how they will be stored within your application. The next figure presents this second screen of the wizard.

![](img/7954dcc7dd1d929d072aec8e9531b6cc_62_0.png)

在之前的截图中，注意到连接字符串和映射详细信息的存储位置将保存在 web.config 文件中。你也可以在这个屏幕上看到，你正在向导底部的文本框中为模型实例命名为 NORTHWINDEntities。这个名称很重要，因为你将在本示例后面使用它。

下一个屏幕允许你选择将成为模型一部分的表、视图或存储过程。对于本示例，请在树视图中选择 Table 项目旁边的复选框以选择数据库中的所有表，如下一图所示。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_62_1.png)

选中 Table 复选框后，单击 Finish 按钮，让 Visual Studio 为你创建 EDM。你会注意到 Visual Studio 会在 O/R Designer 中为你创建模型的视觉表示。

如果查看解决方案中的 `Northwind.designer.vb` 或 `Northwind.designer.cs` 文件，你会看到为你的 EDM 生成的所有代码已就位。此类文件名为 `NORTHWIND.Entities`。

## 创建服务

现在 EDM 和数据库都已就位，下一步是添加你的 WCF 数据服务。为此，在 Visual Studio 解决方案资源管理器中右键单击你的项目，并从提供的菜单中选择 Add ➜ New Item。Add New Item 对话框再次出现；从提供的对话框中间部分选择 WCF Data Service（见下图）。

![](img/7954dcc7dd1d929d072aec8e9531b6cc_63_0.png)

如图所示，将你的 WCF 数据服务命名为 `NorthwindDataService.svc`。完成后，单击 Add 按钮，Visual Studio 将代表你生成一个 WCF 服务。以下列表显示了默认服务文件的代码。

### Pro ASP.NET 9780470502204 Listing 31-33: WCF 数据服务的默认 .svc 文件

```vb
Imports System.Data.Services
Imports System.Linq
Imports System.ServiceModel.Web

Public Class NorthwindDataService
    ' TODO: replace [[class name]] with your data class name

    Inherits DataService(Of [[class name]])

    ' This method is called only once to initialize service-wide
    policies.
    Public Shared Sub InitializeService(ByVal config As
    IDataServiceConfiguration)
        ' TODO: set rules to indicate which entity sets and service
        operations are visible, updatable, etc.
        ' Examples:
        ' config.SetEntitySetAccessRule("MyEntitySet",
        EntitySetRights.AllRead)
        ' config.SetServiceOperationAccessRule("MyServiceOperation",
        ServiceOperationRights.All)
    End Sub

End Class
```

![](img/7954dcc7dd1d929d072aec8e9531b6cc_64_0.png)

```csharp
using System;
using System.Collections.Generic;
using System.Data.Services;
using System.Linq;
using System.ServiceModel.Web;

namespace Web_ADONETDS
{
    public class NorthwindDataService :
        DataService< /* TODO: put your data source class name here */ >
    {
        // This method is called only once to initialize
        // service-wide policies.
        public static void
            InitializeService(IDataServiceConfiguration config)
        {
            // TODO: set rules to indicate which entity sets and
            service operations are visible, updatable, etc.
            // Examples:
            // config.SetEntitySetAccessRule("MyEntitySet",
            //     EntitySetRights.AllRead);
            // config.SetServiceOperationAccessRule
            //     ("MyServiceOperation", ServiceOperationRights.All);
        }
    }
}
```

此处生成的代码是你将通过 WCF 数据服务公开的基础框架。然而，在完成代码中指定的大 TODO 之前，它将无法工作。第一步是使用以下列表中提供的代码输入 EDM 实例的名称。

### PRO ASP.NET 9780470502204 Listing 31-34: 修改 WCF 数据服务以与你的 EDM 配合工作

```vb
Public Class NorthwindDataService
    Inherits DataService(Of NORTHWINDEntities)
    ' Code removed for clarity
End Class
```

```csharp
public class NorthwindDataService : DataService<NORTHWINDEntities>
{
    // Code removed for clarity
}
```

现在你的应用程序处于数据库、EDM 以及用于操作 EDM 的服务都已就位的状态。编译后在浏览器中打开 NorthwindDataService.svc 文件，你会看到以下 XML 片段：

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<service xml:base="http://localhost:4113/NorthwindDataService.svc/"
xmlns:atom="http://www.w3.org/2005/Atom"
xmlns:app="http://www.w3.org/2007/app"
xmlns="http://www.w3.org/2007/app">
  <workspace>
    <atom:title>Default</atom:title>
  </workspace>
</service>
```

如果看不到此 XML，则需要通过选择 Tools ▸ Internet Options 关闭 IE 浏览器的订阅源阅读功能。从提供的对话框中，选择 Content 选项卡，并在 Feeds 部分单击 Select 按钮。从那里，你可以取消选中“Turn on feed reading”复选框。

前面 XML 的结果本应是模型中存在的所有可用集合的列表，但默认情况下，WCF 数据服务会锁定所有内容。要从模型中解锁这些集合，请返回到 `InitializeService()` 函数并添加以下加粗代码，如以下列表所示：

### Pro ASP.NET 9780470502204 Listing 31-35: 打开服务以便从可用表中进行读取

```vb
Imports System.Data.Services
Imports System.Linq
Imports System.ServiceModel.Web

Public Class NorthwindDataService
    Inherits DataService(Of NORTHWINDEntities)

    Public Shared Sub InitializeService(ByVal config _
        As IDataServiceConfiguration)
        config.SetEntitySetAccessRule("*", EntitySetRights.AllRead)
    End Sub

End Class
```

```csharp
using System;
using System.Collections.Generic;
using System.Data.Services;
using System.Linq;
using System.ServiceModel.Web;
using System.Web;

namespace Web_ADONETDS
{
    public class NorthwindDataService : DataService<NORTHWINDEntities>
    {
        public static void
            InitializeService(IDataServiceConfiguration config)
        {
            config.SetEntitySetAccessRule("*",
                EntitySetRights.AllRead);
        }
    }
}
```

在这种情况下，每个表都已打开以供访问。访问这些表的所有人都有读取它们的权限，但没有写入或删除的能力。所有表都是通过使用星号 (*) 指定的，并且底层数据的权限通过将 EntitySetRights 枚举设置为 AllRead 而设为只读。

现在，编译并在浏览器中运行此服务时，你会看到以下 XML 片段：

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<service xml:base="http://localhost:4113/NorthwindDataService.svc/"
xmlns:atom="http://www.w3.org/2005/Atom"
xmlns:app="http://www.w3.org/2007/app"
xmlns="http://www.w3.org/2007/app">
  <workspace>
    <atom:title>Default</atom:title>
    <collection href="Categories">
      <atom:title>Categories</atom:title>
    </collection>
    <collection href="CustomerDemographics">
      <atom:title>CustomerDemographics</atom:title>
    </collection>
    <collection href="Customers">
      <atom:title>Customers</atom:title>
    </collection>
    <collection href="Employees">
      <atom:title>Employees</atom:title>
    </collection>
    <collection href="Order_Details">
      <atom:title>Order_Details</atom:title>
    </collection>
  </workspace>
</service>
```
