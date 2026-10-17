
```csharp
using System.Windows.Shapes;

using ServiceReference1;

namespace MyWpf

{

    /// <summary>

    /// MainWindow.cs 逻辑

    /// </summary>

    public partial class MainWindow : Window

    {

        public MainWindow()

        {

            InitializeComponent();

        }

        private void button1_Click(object sender, RoutedEventArgs e)

        {

            MyWebServiceClient s = new MyWebServiceClient();

            ListViewDetails.DataContext = s.GetData();

        }

    }

}
```

在列表 21.22 中，代码被 `button1` 的点击事件以生成数据。生成的数据由 `MyWebService` 获取。你可以在图 21.30 中看到 `MyWpf` 应用程序的最终输出。

来自 Web 服务的数据

| 员工 ID | 名字 | 姓 | 城市 | 国家 |
|---|---|---|---|---|
| 1 | Nancy | Davis | Seattle | USA |
| 2 | Andrew | Fuller | Tacoma | USA |
| 3 | Janet | Levering | Kirkland | USA |
| 4 | Margaret | Richmond | | USA |
| 5 | Steven | | London | UK |
| 6 | Michael | Suyama | London | UK |
| 7 | Robert | King | London | UK |

图 21.30：从 Web 服务检索数据

# 创建 WCF 数据服务

创建一个名为 `WCFDataService` 的 WCF 数据服务，以便在网页上检索 SQL 数据。
执行以下步骤创建 `WCFDataService` 应用程序：

- 1. 创建 `WCFDataService` 的 ASP.NET 空网站。
- 2. 向 `WCFDataService` 项目添加一个名为 `Default.aspx` 的 Web 表单（Web Form）。
- 3. 将列表 21.23 中的代码添加到 `Default.aspx` 文件。

```xml
<@Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs"
Inherits="Default" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<run runat="server">
<title>Default</title>
</head>
<body>
<form id="form1" runat="server">
<div>
  HELLO WORLD
</div>
</form>
</body>
</html>
```

- 4. 选择 LINQ to SQL Classes 模板，并将 `MyClass.dbml` 文件添加到 `WCFDataService` 项目中，如图 21.31 所示。

> 注意
> 当你添加 `MyClass.dbml` 文件时，会出现一个警告以确认文件的创建。

`MyClass.dbml` 文件已添加到你的项目中，并打开了对象关系设计器（Object Relational Designer）窗口。

- 5. 从服务器资源资源管理器（Server Explorer）窗口中的 `Northwind` 数据库中，将表拖到对象关系设计器窗口中，如图 21.31 所示：

![](img/17af790174c480761404624aeed9b30b_1025_1.png)

图 21.31：添加 Products 表

- 6. 为 `WCFDataService` 项目添加一个名为 `MyDataService.svc` 的 WCF 数据服务，如图 21.32 所示：

## 瞬时解决方案

![](img/17af790174c480761404624aeed9b30b_1026_0.png)

图 21.32：添加数据服务

修改 `MyDataService.cs` 文件的代码，如列表 21:24 所示：

```csharp
Listing 21:24: WCFDataServiceApplication 中 MyDataService.cs文件的代码
using System;
using System.Data.Services;
using System.Data.Services.Common;
using System.Collections.Generic;
using System.Linq;
using System.ServiceModel.Web;
public class MyDataService : DataServiceMyClass
{
    // 此方法被调用一次以初始化服务范围的策略。
    public static void initializeService(DataserviceConfiguration config)
    {
        // TODO: 设置规则指示哪些实体集和操作
        // 示例：
        config.SetEntityAccessRule("Entityset", EntityRights.All);
        config.SetOperationAccessRule("MyOperation", ServiceOperation.All);
        config.DataServiceProtocol = DataServiceProtocolVersion.v2 { errors = true // 仅用于调试 }
    }
}
```

按下 `F5` 键运行 `WCFDataServiceApplication`。当你运行应用程序时，你会发现一个带有 HELLO WORLD 文本的网页。你可以在 Web 浏览器的地址栏中输入以下 Web 地址来检索 Products 的第一条目

`http://localhost:1914/WCFDataServiceSite/MyDataService.svc/Products(1)`

图 21.33 显示了 `WCFDataServiceApplication` 的输出：

# 第21 章：Windows Forms 和 WPF 中的数据绑定

![](img/17af790174c480761404624aeed9b30b_1027_0.png)

图 21.33：在网页上显示数据

> 如果你的浏览器没有显示图 21.32 所示的输出内容，请执行以下步骤：

- 1. 选择“工具”+“Internet ”。打开 Internet 对话框。
- 2. 选择“内容”选项卡。
- 3. 点击“馈送和 Web 切片”图标中的“设置”按钮。出现“馈送和 Web 切片设置”对话框。
- 4. 取消勾选“启用馈送”框并点击“确定”按钮，如图 21.34 所示：

![](img/17af790174c480761404624aeed9b30b_1027_1.png)

图 21.34：显示馈送和 Web 切片设置对话框

现在，让我们总结本章讨论的主要主题。

# 总结

在本章中，你学习了将数据绑定到 Windows Forms 和 WPF 应用程序。你还学习了 Windows Forms 应用程序中的基本数据绑定概念。接下来，你学习了 Windows Forms 应用程序中的数据绑定类型。此外，你还学习了 Windows Forms 应用程序中不同控件。本章还解释了 WPF 的数据绑定概念。接着，你学习了不同的数据源、数据绑定声明以及集合集合。最后，你学习了使用 WCF 数据服务绑定 SQL 数据。这些概念的实际实现涵盖在本章的“瞬时解决方案”部分。

在下一章中，你将学习 ASP.NET 中的数据绑定。

## ASP.NET 中的数据绑定

| 如果你需要针对以下内容的瞬时解决方案： | 参见页码： |
| :--- | :--- |
| 使用 SqlDataSource 控件 | 129 |
| 使用 LinqDataSource 控件 | 135 |
| 使用 ObjectDataSource 控件 | 139 |
| 使用 XmlDataDataSource 控件 | 142 |
| 使用 EntityDataSource 控件 | 145 |
| 使用 GridView 控件 | 150 |
| 使用 DataList 控件 | 154 |
| 使用 DetailsView 控件 | 157 |
| 使用 FormView 控件 | 159 |
| 使用 Repeater 控件 | 162 |
| 使用 ListView 和 DataPager 控件 | 164 |
| 使用 Chart 控件 | 169 |
| 使用 Query/Extender 控件 | 171 |

# 第22 章：ASP.NET 中的数据绑定

## 深入解析

数据库是记录或信息的集合，以系统化的方式以表格的形式存储，以便计算机程序轻松访问所需的信息。结构化查询语言 `SQL` 用于检索、存储和更新记录。应用程序可能需要使用数据库来执行某些功能，例如：

- 从数据库检索记录并以表格格式显示数据
- 在处理数据库的记录后显示数据，例如计算每条记录的持续时间然后显示记录
- 处理检索到的数据并在数据库中更新
- 根据用户指定的选择从数据库中删除记录

在本章中，你将学习 ASP.NET 支持的各种数据源和绑定控件。绑定控件是复合控件。接着，你学习了不同的数据绑定源、数据绑定声明以及向集合绑定数据。最后，你学习了如何使用 WCF 数据服务绑定 SQL 数据。

在本章中，你将学习了 ASP.NET 支持的各种数据源和绑定控件。绑定控件是复合控件。如下

- `GridView` 控件
- `DataList` 控件
- `DetailsView` 控件
- `FormView` 控件
- `Repeater` 控件
- `DataPager` 控件
- `Chart` 控件
- `Query/Extender` 控件
- `SqlDataSource` 控件
- `LinkDataSource` 控件
- `ObjectDataSource` 控件
- `XmlDataDataSource` 控件
- `EntityDataSource` 控件
