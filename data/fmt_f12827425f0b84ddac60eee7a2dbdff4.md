
你可以看到列表 17.5 中的 `select` 子句包含了 `Code`、`ProdName` 和 `Price`。在这里，查询对象中价格>=250 的产品行的所有字段——`Code`、`ProdName` 和 `Price`——都被显示在屏幕上，如图 17.6 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_567_0.png)

**图 17.6** 显示价格大于 $250 的完整 Products 行。

经微软许可使用。

你可能会想，除了控制台应用程序，是否可以创建使用 LINQ 的网站？是的，当然可以！下面的示例创建了一个使用 LINQ 访问 Products 表所有行的网站，并通过 GridView 控件显示它们。

创建一个名为 `LINQToSQLSite` 的空网站。向网站添加一个名为 `Default.aspx` 的 Web Form，并在表单上拖放一个 GridView 控件。要向应用程序添加 DataContext，在解决方案管理器中右键点击应用程序，并选择“添加”，“添加新项”。选择 LINQ to SQL 类模板。将文件名指定为 `ProductsClasses.dbml`，并点击“添加”按钮（见图 17.7）。打开对象关系设计器窗口。从服务器资源管理器中，将 CSharpSampleDatabase 中的 Products 表拖放到设计器表面的左窗格中。这为你的 Products 表及其实体创建了所有映射和设置。它还为 Web.config 文件中为你创建了连接字符串，所示：

```
<connectionStrings>
  <add name="CSharpSampleDatabaseConnectionString" connectionString="Data Source=(local);Initial Catalog=CSharpSampleDatabase;Integrated Security=True" providerName="System.Data.SqlClient" />
</connectionStrings>
```

连接字符串有助于连接 CSharpSampleDatabase 中的 Products 表。现在在 Default.aspx 表单上拖放一个 GridView 控件。要显示价格大于或等于 250 的产品，打开 Default.aspx.cs 文件并编写如列表 17.6 所示的代码。

列表 17.6 Default.aspx.cs 中的程序代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI.Controls;
public partial class _Default : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        ProductsClassesDataContext db = new ProductsClassesDataContext();
        var products = from c in db.Products
        where c.Price >= 250
        select c;
        GridView1.DataSource = products;
        GridView1.DataBind();
    }
}
```

创建了一个名为 `db` 的上下文。通过该上下文访问 Products 表，并将所有价格 >=250 的行分配给 `products`。将 `products` 绑定到 GridView 控件以显示在屏幕上，如图 17.7 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_569_0.png)

**图 17.7** 通过 GridView 控件显示产品。

经微软许可使用。

## 总结

在本章中，你学习了如何在 C# 语言中使用 LINQ。你看到了 LINQ 如何简化代码并轻松执行不同的任务。你探索了隐式类型变量、对象和集合初始化以及 Lambda 表达式等相关功能。你看到了匿名方法、扩展方法和匿名类型如何在 .NET 应用程序中使用。最后，你通过运行应用程序探索了 LINQ to Objects、LINQ to XML 和 LINQ to SQL 等分类。

在下一章中，你将学习如何开发网站以及如何处理会话。你还将学习常用工具及其实现以及如何编写服务。最后，你将学习创建服务端和客户端 ASP.NET 服务并学习测试它们的程序。

# 第 18 章

# .NET 中的 Web应用程序开发

本章包含以下主题：

- 检查 Visual Studio 工具箱

- 构建你的第一个 应用程序

- 使用 CheckBox 控件

- 使用 RadioButton 控件

- 使用 ListBox 控件

- 使用 LinkButton 控件

- 使用 HyperLink 控件

- 使用 WCF

- 创建客户端应用程序

Visual Studio 拥有许多工具，可以让创建网站的任务变得简单得多。为了设计优秀的用户界面，你不需要编写代码；只需要从相应的工具箱中拖放所需的控件并将其放置在表单上即可。从那里，你可以根据需求配置控件。在在 Visual Studio 中开发网站之前，你将查看 Visual Studio 工具箱提供的各种工具。

## 检查视觉工具箱

Visual Studio 2013 中的工具箱分为几个选项卡，如图 18.1 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_572_0.png)

图 18.1

工具箱中的不同工具。

经微软许可使用。

表 18.1 包含了工具箱中不同选项卡的概述。

| 选项卡 | 该区域包含的控件 |

| --- | --- |

| 标准 (Standard) | 包含标准的 <asp:> 控件，例如 TextBox、Button、RadioButton、CheckBox 等，这些通常是标准 Web 应用程序所所需的。 |

| 数据 (Data) | 包含所有处理从任何数据库检索和显示数据的。此部分包括数据源控件 DataSource、AccessDataSource 等，以及用于以表格格式显示检索到的数据的 GridView、DetailsView 和 Datalist。 |

| 验证 (Validation) | 包含所有验证控件，例如 RequiredFieldValidator 和 RegularExpressionValidator，它们在处理用户输入的数据之前对其进行验证。 |

| 导航 (Navigation) | 包含允许用户导航到网站不同页面的所有控件。包括 SitemapPath、Menu 和 TreeView 等控件。这些控件可以在您的网站上提供菜单或以节点形式提供网站页面。用户可以通过从菜单中选择相应的菜单项或从 TreeView 中选择所需的节点来轻松进入任何 Web 表单。 |

| 登录 (Login) | 包含所有处理为 ASP.NET 应用程序添加用户登录和密码功能的控件，例如 Login、CreateUserWizard 和 PasswordRecovery。 |

## 检查 Visual Studio 工具箱

| WebParts | 包含 WebPartManager、WebPartZone 和 CatalogZone 等控件，用于制作门户（具有用户可以自定义的模块化内容的 页面）。 |

| AJAX 扩展 (AJAX Extensions) | AJAX 代表异步 JavaScript 和 XML。这些控件旨在以最少的努力构建高响应的 Web 应用。 |

| 动态数据 (Dynamic Data) | 用于运行时获取架构信息。这些控件还提供了默认的显示格式，并允许您在运行时轻松自定义这些格式。 |

| HTML | 包含超文本标记语言 (HTML) 服务器控件。在进行 ASP.NET 编程时，除了 Web 服务器控件外，您还可以使用 HTML 服务器控件。 |

| 通用 (General) | 留空，以便您可以在其中放置自己的自定义控件。 |

标准工具箱选项卡包含多个控件。下面提到了其中几个常用的控件：

- **Label 控件**——在 Web 表单上显示简单文本，该文本可以是不可见的或可见的，用于向用户显示所需信息。通过 Label 控件显示文本，请使用其 Text 属性。您可以配置 Text、Font、BackColor 和 ForeColor 属性，以所需的字体和颜色显示文本。

- **TextBox 控件**——接受用户输入的数据。在此控件中输入的数据是文本形式的，如果需要，可以通过相应的函数 `Convert.ToInt32()`、`Convert.ToSingle()`、`Convert.ToDecimal()` 等将其转换为整数或浮点数。通过使用此控件的 TextMode 属性，您可以让 TextBox 接受单行或多行文本。通过将 ReadOnly 属性设置为 true，可以避免更改任何 TextBox 的内容。始终可以使用设置 Font、Size、BackColor 和 ForeColor 的功能。

- **Button 控件**——触发事件。通过此控件，当在 Button 控件上发生点击或其他事件时，您可以执行一个语句块。通常情况下，您使用 Button 控件来提交 Web 表单（将数据提交到服务器）。在 ASP.NET 中，有三种类型的按钮：

- **Button**——标准按钮，您通常在 Web 表单上看到作为可点击控件。

- **LinkButton**——行为类似于超链接的按钮，可以帮助您导航到所需的 Web 表单。

- **ImageButton**——在按钮上显示图形图像而不是文本的按钮。换句话说，它是一个图形按钮。

- **DropDown List 控件**——向用户显示选项列表。此控件占的空间较少，因为它在不使用时处于折叠模式。

- **ListBox 控件**——提供一个固定大小的项目列表供用户选择。

- **CheckBox 和 RadioButton 控件**——CheckBox 允许您选择一个选项。相反，RadioButton 控件是互斥的，这意味着您只能从一组可用选项中选择其中一个。

- **HyperLink 控件**——帮助您导航到同一网站的另一个 Web 表单或互联网上的任何其他资源。

- **Image 控件**——在页面上显示图像。

- **Calendar 控件**——在您的 Web 表单上显示功能全的日历。您可以轻松移动到任何月份并选择任何特定日期。您可以双击任何一天来检索它。要获取您所需格式的日期，可以使用多种方法，包括 `ToLocalTime` 和 `ToDateString`。

您可以通过附加到每个控件的属性配置每个控件。此外，每个控件都有与其相关的特定事件。这些事件与相应的事件处理器关联，以便在事件发生时采取操作。例如，点击事件与 Button 控件关联，当用户点击它时就会触发该事件。每个事件由该方法中的一个唯一方法表示。您在事件发生时想要执行的代码必须写在该方法中。例如，`Button1_Click()` 方法与 `Button1` 控件关联，它在发生点击时被调用。

几乎所有控件都有某些共同属性，表 18.2 简要描述了这些属性

| 表 18.2 控件的常用属性 |

| 属性 | 描述 |

|---|---|

| AccessKey | 为任何控件分配快捷键。如果您为任何控件分配 AccessKey（例如 b），可以使用快捷键 Alt+b 访问该控件。 |

| BackColor | 控制所选控件的背景颜色。 |

| BorderColor | 为控件边缘分配指定的颜色。 |

| BorderWidth | 指定边框的像素宽度。 |

| BorderStyle | 为边框分配设计。默认情况下，边框被创建为实线，但提供了多种样式，如 Dotted、Dashed、Solid、Double、Groove、Ridge、Inlet 和 Outset。 |

| Enabled | 启用或禁用任何控件。如果 Enabled 设置为 false，则控件被禁用（意味着控件上不会发生事件）。默认情况下，Enabled 属性设置为 true。 |

| EnableTheming | 允许您开启所选控件的功能。默认值为 true。 |

| Font | 设置在控件中显示的文本的字体。 |

| ForeColor | 设置控件上显示的文本的前景颜色。 |

| Height | 设置控件的高度。 |

| SkinID | 设置在对控件应用主题时使用的皮肤。 |

| CssClass | 允许您为控件应用 CSS（级联样式表）类。 |

| TabIndex | 设置控件在 ASPNET 页面上的制表顺序。此属性与页面上的其他控件配合使用。 |

| ToolTip | 为选定的控件分配 Tool，向用户提供有关控件的信息。 |

| Width | 设置控件的宽度。 |

## 第 18 章使用 .NET 开发 Web 应用程序

在 Web 表单中使用任何控件后，Visual Studio 会自动生成表示该控件以及对其设置的属性属性代码。例如，当您将 Button 控件拖放到 Web 表单时，会生成生成以下代码：

`<asp:Button ID="btnCalculate" runat="server" Text="Calculate Bill"/>`

前面的陈述告诉您 `btnCalculate` 是 Button 控件的 ID。唯一的 ID 对于识别和访问控件至关重要。`runat` 属性表示此控件是服务器控件（它在服务器上执行，而不是在客户端机器上）。`Text` 属性表示 Button 控件的标题为 Calculate Bill。

# 第 18 章 ■ 使用 .NET 开发 Web 应用程序

服务器控件关联了某些事件，这些事件指定了当控件上发生特定事件时想要执行的代码。以下代码表示当 Button 控件发生点击事件时，将调用 `btnCalculate_Click` 方法：

```aspx
<asp:Button ID="btnCalculate" runat="server" Text="Calculate Bill" OnClick="btnCalculate_Click" />
```

现在你已经了解了基础控件，并将开始开发小型网站。

## 构建你的第一个 Web 应用程序

你将创建一个网站，用户可以在其中输入产品名称、购买数量和产品价格。点击“Calculate Bill”按钮后，将显示购买产品的账单（价格*数量）。

要创建一个新的空网站，启动 Visual Studio 并选择“文件”、“新建项目”、“Web 网站”。在左侧选项卡选择 Visual C# 语言，在右侧选项卡选择 ASP.NET 网站模板。为网站命名为 `CalculateBillApp` 并点击确定，如图 18.2 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_576_0.png)

**图 18.2** 创建名为 CalculateBillApp 的新网站。

经 Microsoft 许可使用。

最初，你的网站是空的，因此你至少需要一个 Web Form来创建界面。你可以通过在解决方案管理器中右键点击它，并在弹出菜单中选择“添加”、“新建项”，向网站添加一个名为 `Default.aspx` 的 Web 表单。添加 Web 表单后，其后代码文件 `Default.aspx.cs` 会自动添加到你的 `CalculateBillApp` 网站中。

ASP.NET 提供两种类型的编码样式：

- **内联编码（Inline coding）**——在这种编码样式下，同一个文件包含标准的 HTML 代码、定义 Web 表单上服务器控件的 Active Server Pages (ASP) 标签，以及控制 Web 表单上控件操作的代码。

- **后代码文件（Code-behind file）**——在这种编码样式下，Web 表单被分为两个文件。第一个文件包含标准的 HTML 代码和定义 Web 表单上服务器控件的 ASP 标签，该文件以 `.aspx` 扩展名保存。第二个文件包含所选编程语言的代码，用于控制 Web 表单上控件的操作。该文件以 `.aspx.cs` 扩展名保存（因为你在本书中使用的是 C# 编程语言），并被称为后代码文件，因为它提供了 Web 表单背后的代码。

你可以通过以下三种模式打开 Web 表单：

- **设计（Design）**——创建用户界面。在设计模式下，你可以将控件拖放到 Web 表单上。

- **代码（Code）**——显示为拖放到 Web 表单的控件自动生成的代码。代码还代表了与控件相关的属性和事件。

- **拆分（Split）**——允许在拖放控件的同时显示生成的代码。

你以设计模式打开 `Default.aspx` Web 表单，并在其上拖放了五个 Label、四个 TextBox 和一个 Button 控件，如图 18.3 所示。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_578_0.png)

图 18.3 放置在 CalculateBillApp 网站 Default.aspx Web 表单中的控件。

经 Microsoft 许可使用。

将 `Label1` 控件的 Text 属性设置为“Online Store”，如图 18.4 所示。同时，将它的 Font 设置为 X-Large，并将 Bold 属性设置为 True。

![](img/3ca47f8f6f5560f07650d3563e2f2c05_578_1.png)

图 18.4 设置 Label1 控件的 Text 属性。

经 Microsoft 许可使用。

同样，设置 Label 和 Button 控件的 Text 属性，如表 18.3 所示。

| 表 18.3 设置控件的 Text 属性 |

| 控件 | Text 属性 |

| --- | --- |

| Label2 | Product Name |

| Label13 | Quantity |
