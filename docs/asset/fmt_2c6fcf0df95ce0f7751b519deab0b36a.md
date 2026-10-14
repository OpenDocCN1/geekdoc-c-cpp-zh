
| | |
|---|---|
| Visual Studio 2010 Professional Edition | Designed for individual developers who want to build a wide variety of Windows, Web, mobile, and Office-based solutions. |
| Visual Studio 2010 Premium Edition | Designed for individuals and teams who want to build scalable applications and includes standard testing tools, database deployment and change-management tools, and basic lifecycle management tools. |
| Visual Studio 2010 Ultimate Edition | Designed for teams and includes full testing, modeling, database, and lifecycle management tools. |

## Description

- 要开发 ASP.NET 4 应用程序，你需要在自己的 PC 上安装上面显示的客户端软件。此外，如果你没有单独的服务器可用，你通常还需要 IIS 和数据库服务器，例如 SQL Server 2008 Express Edition。有关更多信息，请参阅图 1-8。

- Visual Studio 2010 有四个不同的版本，提供开发 ASP.NET 应用程序所需的所有基本功能。你选择的版本取决于你需要的额外功能。

## .NET Framework 的组件

因为在开发应用程序时，你应该对 .NET Framework 的作用有一个基本的了解，图 1-7 总结了其主要组件。正如你所见，该框架分为两个主要组件，.NET Framework 类库和通用语言运行时，而这些组件为用 Visual Basic 或 C# 等 .NET 语言编写的应用程序提供了一组通用的服务。

.NET Framework 类库由提供开发 .NET 应用程序所需许多功能的类组成。例如，ASP.NET 类用于开发 ASP.NET Web 应用程序，而 Windows Forms 类用于开发标准的 Windows 应用程序。其他 .NET 类让你可以处理数据库、管理安全、访问文件并执行许多其他功能。

尽管在该图中并不明显，但 .NET Framework 类库中的类是按层次结构组织的。在此结构中，相关的类被组织成称为命名空间的组。每个命名空间都包含用于支持特定功能的类。例如，`System.Web` 命名空间包含用于创建 ASP.NET Web 应用程序的类，而 `System.Data` 命名空间包含用于访问数据的类。

通用语言运行时，或 CLR，提供使用 .NET 语言开发的任何应用程序执行所需的服务。这是因为所有 .NET 语言都编译为通用的中间语言（或 IL）。CLR 还提供通用类型系统，该系统定义了所有 .NET 语言使用的数据类型。这样，无论你使用哪种 .NET 语言开发应用程序，都可以使用相同的数据类型。

要运行 ASP.NET 应用程序，Web 服务器必须安装 .NET Framework。但是，访问 Web 服务器的客户端计算机不需要 .NET Framework。相反，客户端计算机可以运行任何具有现代 Web 浏览器的客户端操作系统。

## .NET Framework

![](img/c024ccf88e28c30c07dd410d4342288f_36_0.png)

### 描述

- .NET 应用程序通过使用 .NET Framework 的服务来工作。.NET Framework 反过来访问操作系统和计算机硬件。

- .NET Framework 由两个主要组件组成：.NET Framework 类库和通用语言运行时。

- .NET Framework 类库以类的形式提供预先编写的代码，这些类可供所有 .NET 编程语言使用。这些类被组织成称为命名空间的组。支持 ASP.NET Web 程序的类存储在 `System.Web` 命名空间中。

- 通用语言运行时，或 CLR，通过协调内存管理、代码执行、安全性和其他服务等基本功能来管理 .NET 程序的执行。

- 通用类型系统是 CLR 的一个组件，可确保所有 .NET 应用程序无论使用何种编程语言开发，都使用相同的数据类型。

- 所有 .NET 程序都编译为 Microsoft 中间语言（MSIL）或仅为中间语言（IL），该语言以程序集的形式存储在磁盘上。然后由 CLR 运行该程序集。

## 开发 ASP.NET 应用程序的三种环境

图 1-8 显示了用于编码和测试 ASP.NET 应用程序的三种常见开发环境设置。正如你将看到的，每种设置都有其优点和缺点。你选择的环境将取决于你的开发需求和可用的资源。

最简单的开发环境是独立环境。在这种情况下，一台计算机同时充当客户端和服务器。因此，它必须运行支持 ASP.NET 开发的操作系统，并且必须安装 .NET Framework 和 Visual Studio 2010。由于 Visual Studio 2010 附带了用于本地测试的自己的开发服务器，因此在使用独立环境时你不必安装 IIS。此外，由于 Visual Studio 附带 SQL Server 2008 Express Edition（或仅为 SQL Server Express），因此你不必安装单独的数据库产品。这是我将在本书中重点介绍的环境。

第二个开发环境使用通过局域网连接的独立客户端和服务器计算机。在这里，客户端计算机安装了 Windows、.NET Framework 和 Visual Studio 2010，而服务器运行 Windows Server 并安装了 .NET Framework、IIS 和 FrontPage Server Extensions（FPSE）。FPSE 提供 Visual Studio 2010 用于与远程计算机上的 Web 站点通信的服务。此外，服务器使用 SQL Server 来处理数据库访问。借助此环境，多个程序员可以同时处理同一个应用程序，但所有程序员都位于同一站点。

在第三种开发环境中，客户端计算机通过 Internet 而不是 LAN 连接到服务器。这使得可以与托管在另一台服务器上的 Web 站点一起工作。此环境需要 FTP 服务器，用于在客户端计算机和服务器之间复制 Web 站点中的文件。FTP 服务器使用文件传输协议（FTP）执行复制操作，并且可以配置 IIS 以充当 FTP 服务器以及 Web 服务器。因此，如果 Web 站点托管在你有权访问的服务器上，则可以配置服务器以便远程用户可以使用 FTP 访问它。

![](img/c024ccf88e28c30c07dd410d4342288f_38_0.png)

![](img/c024ccf88e28c30c07dd410d4342288f_38_1.png)

![](img/c024ccf88e28c30c07dd410d4342288f_38_2.png)

### 描述

- 当你使用独立开发时，一台计算机同时充当客户端和服务器。由于 Visual Studio 附带了一个精简的 Web 服务器，称为 ASP.NET 开发服务器（或仅为开发服务器），因此你无需使用 IIS 在自己的 PC 上测试 Web 应用程序。但是，你确实需要使用 IIS 来测试 Web 应用程序的某些功能。

- 当你使用 *局域网*（LAN）时，客户端计算机通过 LAN 与服务器计算机通信。借助此设置，同一站点的两个或多个程序员可以同时处理同一个应用程序。此设置要求在服务器上安装 *FrontPage Server Extensions*（FPSE）。

- 当你使用 Internet 开发时，客户端计算机通过 Internet 与服务器计算机通信。借助此设置，不同位置的程序员可以同时处理同一个应用程序。此设置要求服务器上安装 *FTP 服务器*。FTP 服务器使用 *文件传输协议*（FTP）在客户端计算机和服务器之间传输文件。

![](img/c024ccf88e28c30c07dd410d4342288f_38_3.png)

## ASP.NET 应用程序工作原理的快速预览

有了这些背景知识，你就可以了解 ASP.NET 应用程序的工作原理了。因此，本主题提供了 Shopping Cart 应用程序中 `Order` 表单工作原理的快速预览。

### Shopping Cart 应用程序使用的文件

图 1-9 以在 Visual Studio 2010 中使用 Web 窗体设计器开发 Web 窗体时显示的方式呈现了 Shopping Cart 应用程序的 Order 表单。在第 2 章中，你将学习如何使用此设计器，但现在只需尝试了解此表单的工作原理的整体情况。

如果你查看 IDE 中间的设计器窗口，你可以看到用于此表单的表格以及用于显示每个产品数据的标签控件。你还可以看到已使用下拉列表的智能标记菜单来启用 `AutoPostBack` 属性。这意味着当用户从下拉列表中选择一个项目时，`Order` 表单将被发布回 Web 服务器。

如果你查看设计器窗口右侧的解决方案资源管理器，你可以看到此应用程序所需的文件夹和文件。现在，只需关注此图中表格中总结的七个代码文件。表中前三个文件位于 `App_Code` 文件夹中，表示名为 `CartItem`、`CartItemList` 和 `Product` 的业务类。这三个文件都以 `cs` 为扩展名，这意味着它们是 C# 文件。

表中的接下来的四个文件用于两个 Web 窗体 `Cart` 和 `Order`，每个窗体有两个文件。扩展名为 `aspx` 的文件（`Cart.aspx` 和 `Order.aspx`）包含表示表单设计的代码。此代码由标准 HTML 代码加上定义表单上使用的服务器控件的 `asp` 标签组成。我们将此称为 `aspx` 代码，因为包含代码的文件具有 `aspx` 扩展名。

另外两个文件，扩展名为 `aspx.cs`，包含控制表单操作的 C# 代码。这些称为代码隐藏文件，因为它们提供了 Web 表单背后的代码。例如，`Order.aspx.cs` 文件是 `Order` 表单的代码隐藏文件。

在继续之前，你应该意识到不必将 Web 表单的 `aspx` 和 C# 代码存储在单独的文件中。相反，ASP.NET 允许你将此代码合并到单个 `aspx` 文件中。但是，将 `aspx` 和 C# 代码存储在单独的文件中可以简化应用程序开发，因为它让你可以将页面的表示元素与其 C# 编码分开。这也使得 HTML 设计师能够处理应用程序的 `aspx` 文件，然后让 C# 程序员开发代码隐藏文件的代码。

### 设计视图中的订单表单

![](img/c024ccf88e28c30c07dd410d4342288f_40_0.png)

### 购物车应用程序中的 `aspx` 和 C# 文件

| 文件夹 | 文件 | 说明 |
|---|---|---|
| `App_Code` | `CartItem.cs` | 表示购物车中某个商品项的类。 |
| `App_Code` | `CartItemList.cs` | 表示购物车中所有商品项的类。 |
| `App_Code` | `Product.cs` | 表示商品的类。 |
| （根目录） | `Cart.aspx` | 购物车页面的 `aspx` 文件。 |
| （根目录） | `Cart.aspx.cs` | 购物车页面的代码隐藏文件。 |
| （根目录） | `Order.aspx` | 订单页面的 `aspx` 文件。 |
| （根目录） | `Order.aspx.cs` | 订单页面的代码隐藏文件。 |

### 说明

- 对于应用程序中的每个 Web 窗体，ASP.NET 4 会维护两个文件。扩展名为 `.aspx` 的文件包含 HTML 代码和用于服务器控件的 `asp` 标记。扩展名为 `.aspx.cs` 的文件是 *代码隐藏文件*，其中包含该窗体的 C# 代码。

- 如果 ASP.NET 4 应用程序还需要其他类（如 *业务类*），它们将保存在 `App_Code` 文件夹中。

![](img/c024ccf88e28c30c07dd410d4342288f_40_1.png)

## 订单表单的 `aspx` 代码

为了让你对 aspx 代码的运作方式有所了解，图 3-10 显示了订单表单的部分 aspx 代码。所有这些代码都是你在使用 Web Forms 设计器设计窗体时由 Visual Studio 生成的，因此你无需手动编写。但你仍应对这些代码的运作方式有一个大致的了解。

每个 Web 窗体的第一组标记定义了一个 *页面指令*，它提供了四个 *属性*。在这里，`Language` 属性指明语言为 C#，`CodeFile` 属性指明代码隐藏文件名为 `Order.aspx.cs`，`Inherits` 属性指定名为 `Order` 的类。在图 3-11 中，你将看到 `Order` 类如何继承 `Page` 类。

第二组标记定义了一个 `DOCTYPE` 声明，它告诉浏览器文档使用的是哪个版本的 HTML。你暂时可以忽略这个声明，因为在第 5 章中你会学到更多相关内容。

`html` 标记标记 HTML 文档的开始和结束，`head` 标记定义文档的标题部分。在这里，`title` 标记定义页面运行时显示在浏览器标题栏中的标题。另外，`style` 标记定义页面使用的样式。正如你将在第 5 章中学到的，这只是定义样式的一种方式。

网页本身的内容定义在 `div` 标记内，而 `div` 标记位于 `body` 和 `form` 标记内。请注意，第一个 `form` 标记包含一个值为 `"server"` 的 `runat` 属性。这表示该窗体将由 ASP.NET 在服务器上处理。所有 ASP.NET Web 窗体和所有 ASP.NET 服务器控件都需要此属性。

`div` 标记内的 `asp` 标记定义了页面上显示的服务器控件。由于这些控件包含值为 `"server"` 的 `runat` 属性，它们将由 ASP.NET 在服务器上处理。此处理的最后阶段是 *呈现* 控件，这意味着 `aspx` 代码会被转换为标准 HTML，以便浏览器能够显示页面。

如果你查看下拉列表的 `aspx` 代码，可以看到 `AutoPostBack` 属性已设置为 `True`。这意味着，只要用户从该列表中选择了一个项，就会发生回发。请注意，只要用户单击“Add to Cart”按钮，也会发生回发。但是，该控件不需要 `AutoPostBack` 属性，因为执行回发是按钮的默认操作。

尽管 “Add to Cart” 按钮的 `aspx` 代码不包含 `AutoPostBack` 属性，但它确实包含一个 `OnClick` 属性。此属性指定当用户单击按钮并将窗体回发到服务器时执行的事件处理程序。

另一个值得注意的属性是 `aspx` 代码中最后一个按钮的 `PostBackUrl` 属性。此属性提供了 `Cart.aspx` 文件的路径，这意味着当单击此按钮时将请求购物车窗体。这是在应用程序运行过程中从一个窗体切换到另一个窗体的一种方式，你将在下一张图中看到另一种方式。

尽管这只是对 Web 窗体 `aspx` 代码的简要介绍，但你应开始明白这些代码如何定义一个网页。不过，在接下来的两章中，你将学到更多关于这些代码的内容。而且，以防你需要，第 5 章会提供一份完整的 HTML 速成课程。

## 订单表单的 `aspx` 文件（`Order.aspx`）
