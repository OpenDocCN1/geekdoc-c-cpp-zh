

### 1. 应用程序配置文件

部署和安装应用程序时，无需在要使用的设备上准备任何预配置文件。桌面版 Framework 在 System.Configuration 命名空间中包含 ConfigurationSettings 类。该类用于从与应用程序关联、名为 appname.exe.config 的 XML 文件中读取应用程序设置。Compact Framework 不支持该类，但开发者可以使用 System.Xml 命名空间中的类编写自己的实现。

### 2. 方法重载

重载方法提供了调用该方法的其他方式，同时也会增大 Framework 的体积。因此，.NET Compact Framework 几乎移除了所有方法的重载。这有两层含义。第一，在开发基于 .NET Compact Framework 的应用程序时，桌面应用程序中使用的某个特定重载方法很可能不可用。第二，查阅文档时，开发者会密切关注某个方法是否受 .NET Compact Framework 支持。

### 3. 缺失的控件

许多 .NET Framework 控件在 .NET Compact Framework 中不受支持。对移动开发者而言，这些控件中的大多数缺失并不重要。由于打印在移动应用中的作用非常有限，移除整个打印相关控件系列并不是问题。这涉及 CrystalReportViewer、PageSetupDialog、PrintDialog、PrintDocument、PrintPreviewControl 和 PrintPreviewDialog 控件。可以使用自己的对话框，或通过 Windows CE API 直接访问系统对话框，来替代许多缺失的对话框。第三方控件已经陆续出现，以填补 .NET Compact Framework 中遗漏的控件。

### 4. XML 功能

尽管 .NET Compact Framework 在 XML 方面提供了不少功能，但同样多的功能也被移除了。缺失的关键 XML 相关组件是 System.Xml.XPath 命名空间。XPath 命名空间使 XML 解析远比 .NET Compact Framework 提供的方法容易得多。在缺少它的情况下，可以结合使用针对文档对象模型（DOM）的递归搜索和迭代搜索。

.NET Compact Framework 还缺少另一个关键 XML 组件，即可扩展样式表语言转换（XSLT）。借助 XSLT，可以将 XML 文档转换为不同格式。此外，.NET Compact Framework 目前不支持开发基于设备的 XML Web 服务。

### 5. 数据库支持

Compact Framework 省略了 System.Data.OleDb 命名空间，因此不支持使用 OleDb .NET 数据提供程序直接调用数据库。不过，SQL Server CE 的远程数据访问（RDA）功能确实支持从可作为其他数据源数据存储库的 SQL Server 拉取数据。.NET Compact Framework 提供了一套强大的数据相关工具。为 SQL Server CE 提供本地数据库支持。在服务器端，.NET Compact Framework 提供对 SQL Server 的支持。需要注意的是，已有第三方提供用于处理 Pocket Access 数据库的 .NET Compact Framework 组件。

### 6. 二进制序列化

出于大小和性能方面的考虑，BinaryFormatter 和 SoapFormatter 这两个类都已从 .NET Compact Framework 中省略。

### 7. 访问 Windows 注册表

.NET Framework 具有 Microsoft.Win32.Registry 命名空间，使应用程序可以轻松操作 Windows 注册表。显然，该命名空间未包含在 .NET Compact Framework 中，因为它与 Win32 相关，而不是 Windows CE。可以通过调用相关的 Windows API 来访问 Windows CE 注册表。

### 8. 利用 COM 组件与互操作性

将 COM 对象集成到基于 .NET Compact Framework 的应用程序中需要两个步骤。第一步是编写一个非托管代码（即 eMbedded Visual C++）DLL 包装器，以公开该 COM 对象。根据 COM 对象的复杂程度，这项工作可能从简单到极其复杂不等。第二步是使用 PInvoke 访问该 DLL 包装器。目前，庞大的开发社区已经开始致力于访问更常用的 COM 组件，这对所有从事这一领域的开发者都很有帮助。

### 9. 安全性

.NET Compact Framework 不提供对非托管代码的安全访问。任何应用程序都可以调用任何系统或非系统 API。目前 .NET Compact Framework 没有基于角色的安全性。主体对象无法识别已知身份或已知角色。

### 10. XML Web 服务和 System.Web 命名空间

.NET Compact Framework 的 XML Web 服务功能中最显著的缺失是使用 Cookie 的能力。Cookie 被广泛用于在客户端多次调用之间维护服务器上的状态。虽然 Cookie 在 Web 服务中的使用不如在网站上那么普遍，但它们仍在使用。.NET Compact Framework 在 Web 服务方面提供有限的加密能力。不支持 System.Web 命名空间。

### 11. 打印

.NET Compact Framework 不提供打印支持。没有简便方法通过 IR 与网络打印机或外部打印机交互。访问网络打印机的变通方法是构建基于服务器的应用程序，该程序接受并打印任何移动应用程序提交的作业。可以通过 IR 端口将输出直接发送到支持 IR 的打印机。可以使用 System.Net.IrDA 命名空间访问设备的 IR 端口。

### 12. GDI+

Windows CE 原生不支持 GDI+，因此已从 .NET Compact Framework 中移除 GDI+ 相关功能。

### 13. 远程编程

.NET Compact Framework 的第一个版本不支持远程编程。

## 28.1.7 Windows Compact Edition - 项目类型

-   如图 28.1.3 所示，有四种项目类型面向 Windows CE 平台。它们分别是 Windows 应用程序、类库、控制台应用程序和空项目。

![](img/3005a4307e6d8f3bb7e76eea28a92357_892_0.png)

图 28.1.3 Windows CE 项目类型

-   **1. Windows 应用程序**——一个基于 Windows Forms 的项目，包含 Windows CE .NET 特定的控件。这是最常用的模板，因为它生成基于 Windows 的应用程序。
-   **2. 类库**——类库允许将相关组件打包到单个文件中。它们可用于开发其他应用程序，或作为其他组件继承的基础。此项目类型最适合创建可在多个应用程序中复用的代码模块。
-   **3. 控制台应用程序**——用于创建将在控制台窗口中运行的可执行文件。最适合用于后台和维护应用程序，这些程序可能需要也可能不需要用户交互。与 Pocket PC 不同，Windows CE 原生支持控制台应用程序。
-   **4. 空项目**——定义一个没有预定义组件的项目，允许从头开始自定义构建所有内容。

## 28.1.8 .NET Compact Framework - 应用程序架构

-   .NET Compact Framework 应用程序由以下模块组成，这些模块会针对各种类型的设备捆绑为单个应用程序。

![](img/3005a4307e6d8f3bb7e76eea28a92357_893_0.png)

-   除了从本机操作系统服务中抽象出来之外，这些应用程序还继承了其他优势，例如故障隔离、安全性和更好的资源管理，因为它们运行在独立的应用程序域宿主中。目前，.NET Compact Framework 支持 Pocket PC 和基于 Windows CE .NET 的平台。

## 28.1.9 .NET Compact Framework - 支持的语言

-   .NET Compact Framework 支持两种开发语言：C# .NET 和 Visual Basic .NET。虽然早期版本的 Windows CE 开发工具偏爱基于 C 的语言——即 eMbedded Visual C++——但在 .NET Compact Framework 中，选择哪种语言几乎没有区别，因为两者同样强大且功能完备。
-   作为 Visual Studio .NET 开发环境后期新增的语言，J# 不受 .NET Compact Framework 支持。
-   开发者还应注意，.NET Compact Framework 下存在另一项 .NET Framework 下不存在的语言限制。在 .NET Framework 下，可以在单个项目中使用混合语言组件。相比之下，.NET Compact Framework 项目被限制为单一语言，即 C# .NET 或 Visual Basic .NET。针对 .NET Compact Framework 施加的单语言项目限制，变通方法是使用类模板创建额外项目。需要将另一种语言的代码添加到该模板中，然后在应用程序项目中直接添加对这些类的引用。

## 28.1.10 .NET Compact Framework - 在线文档

Visual Studio .NET 附带的文档提供了与 .NET Compact Framework 相关的信息。其中既有 .NET Compact Framework 专属主题，例如“使用 .NET Compact Framework 创建自定义控件”，也有对 .NET Compact Framework 所支持功能的逐项标识。

## 28.1.11 .NET Compact Framework IDE - 附加功能

除了 Visual Studio .NET 原生提供的所有功能之外，.NET Compact Framework 还支持以下设备特定功能：

-   **1. 模板**——常见项目类型的预定义配置。为 Pocket PC 和 Windows CE 设备都提供了模板。
-   **2. 设备特定控件**——专为配合 Pocket PC 和 Windows CE 使用而设计的控件。其界面、资源消耗和功能均已针对这些环境进行定制。
-   **3. 设备模拟器**——模拟特定设备的测试环境。模拟器在开发者的 PC 上运行，允许在没有设备的情况下进行测试。
-   **4. 应用程序自动部署**——可轻松针对模拟器或设备进行测试，为开发者提供无缝的测试环境。

