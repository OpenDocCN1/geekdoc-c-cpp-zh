
### 3. 使用 Visual Studio.NET 和 ADO.NET 工具和向导，通过 `SelectWizardProject` 项目中的 `Student Form` 对 `Student` 表进行数据更新（该项目文件位于 CRC Press ftp 网站 `Students` 文件夹下的 `DB Projects\Chapter 7\SelectWizard Solution` 文件夹中，参见第 1 章图 1.2）。

**提示 1：** 示例数据库中，`Student` 表中所有 `TextBoxes` 到 `Student` 表中所有列的绑定已经完成，并生成了相关组件。

**提示 2：** 使用数据设计器（Data Designer）构建查询函数 `UpdateStudent()`。

**提示 3：** 在 `Student.cs` 代码窗口中，在 `Update` 按钮的 `Click` 方法内部编写代码，以调用查询函数来执行此数据更新。

### 4. 使用运行时对象（Runtime objects），通过 `RTUpdateDelete` 项目完成 `Student Form` 对 `Student` 的数据查询（该项目文件位于 CRC Press ftp 网站 `Students` 文件夹下的 `DB Projects\Chapter 7\UpdateRequestDelete` 文件夹中，参见第 1 章图 1.2）。

### 5. 使用存储过程，通过 `SPUpdateDeleteProject` 项目完成 `Course Form` 对 `Course` 的数据更新查询（该项目文件位于 CRC Press ftp 网站 `Students` 文件夹下的 `DB Projects\Chapter 7\SPUpdateDeleteSolution` 文件夹中，参见第 1 章图 1.2）。

**提示：** 练习中可以使用练习 2 中的代码结合内置的存储过程 `dbo.UpdateCourse`。

### 6. 使用 LINQ to SQL，通过 `LINQSelectProject` 项目完成 `Student Form` 对 `Student` 的数据删除（该项目文件位于 CRC Press ftp 网站 `Students` 文件夹下的 `DB Projects\Chapter 7\LINQSelect Solution` 文件夹中，参见第 1 章图 1.2）。

**提示 1：** 建议删除新插入的学生成员以避免复杂的的数据恢复过程。一种好方法是运行第 6 章作业中的任何练习项目（例如练习 3、4 或 5），插入一个具有以下信息的新学生成员（然后删除此新插入的记录）：

| Student ID | 83658 |
| :--- | :--- |
| Student Name | Susan Bai |
| GPA: | 3.88 |
| Credits: | 96 |
| Major | Computer Science |
| SchoolYear: | Junior |
| Email: | sbai@college.edu |
| image: | White.jpg |

**提示 2：** 如果删除原始学生记录，则涉及四张表的数据删除：`Student`、`Login`、`Course` 和 `StudentCourse`。恢复顺序是：首先从父表（`Student` 表）中恢复记录，然后恢复所有其他子表的所有记录。

# 8 在 ASP.NET 中访问数据

在前面的章节中，我们已经通过基于 Windows 的应用程序对使用 Visual C# 的数据库编程进行了详细讨论。从本章开始，我们将集中于基于 Web 的应用程序使用 Visual C# 进行数据库编程。要开发 Web 应用并允许用户通过互联网访问数据库，你需要理解一个重要的组件：Active Server .NET 或 `ASP.NET`。

本质上，`ASP.NET` 允许用户使用 Web 浏览器编写软件，而不是安装在计算机上的程序。在 `ASP.NET` 的帮助下，用户可以轻松创建和开发 `ASP.NET` Web 应用并作为服务器端项目运行。用户随后可以向服务器发送请求以下载任何页面，通过 Web 浏览器访问数据库以检索、显示和操作数据。客户端与服务器通信实际使用的语言是超文本标记语言（HTML）。完成本章后，你将能够：

- 理解 `ASP.NET` 应用程序的结构和组件。
- 理解 `.NET Framework` 的结构和组件。
- 从数据库中选择数据并在 Web 页面中显示。
- 理解 `Application` 状态结构并实现全局变量的存储。
- 理解 `AutoPostBack` 属性并实现与服务器有效通信。
- 通过 Web 页面从数据库中插入、更新和删除数据。
- 使用存储过程通过 Web 应用对数据库执行数据操作。
- 使用 `LINQ to SQL` 查询通过 Web 应用对数据库执行数据操作。
- 在 Web 页面中执行客户端数据验证。

为了帮助读者成功完成本章，我们首先需要对 `ASP.NET` 进行详细讨论。对于所有不熟悉这一概念的读者来说，对 `ASP.NET` 进行历史回顾是一个重要问题。

## 8.1 ASP.NET 框架的历史回顾

第一个版本 `ASP.NET 1.0` 于 2002 年与 `Visual Studio 2002` 同时发布。由于它一直与 `Visual Studio` 同时发布，确切地说是与 `.NET Framework (4.8)` 同时发布，直到 2019 年发布 `ASP.NET 4.8`。此后，开发了一个名为 `ASP.NET Core` 的 `ASP.NET` 分支；第一个版本是 2016 年构建的。`ASP.NET Core` 的最新版本是 2021 年 11 月发布的 6.0。

`ASP.NET Core` 是一个跨平台框架，它允许任何应用程序运行在不同的平台上，例如 Windows、macOS 和 Linux。与传统的 `ASP.NET 4.x` 相比，`ASP.NET` 提供了一些优势，使用户能够以更高的性能构建 Web 应用程序。然而，对于大多数 Web 应用，可以使用 `ASP.NET 4.x` 框架开发类似的功能，区别在于使用了 `.NET Framework` 运行时。

## 12 使用 C# 进行 SQL Server 数据库编程

`ASP.NET 4x` 和 `ASP.NET Core` 的另一个区别在于，`ASP.NET 4x` 使用 `.NET Framework` 运行时，而 `ASP.NET Core` 使用 `.NET Core`。

`ASP.NET Core` 是一个跨平台框架，它允许任何应用程序运行在不同的平台上，例如 Windows、macOS 和 Linux。与传统的 `ASP.NET 4.x` 相比，`ASP.NET` 提供了一些优势，使用户能够以更高的性能构建 Web 应用程序。然而，对于大多数 Web 应用，可以使用 `ASP.NET 4.x` 框架开发类似的功能，区别在于使用了 `.NET Framework` 运行时。

尽管 `ASP.NET Core` 提供了一些优势，如跨平台和云端开发，但第三方语言限制在 C# 和 F#，它不支持带有用户界面的桌面应用程序。因此，在本书中我们将集中学习 `ASP.NET 4x` 并使用它构建 Web 应用。

开发 `ASP.NET` 的前提条件是 `.NET Framework`，它是 `.NET Framework` 的一部分；换句话说，`.NET Framework` 是 `ASP.NET` 的基础。因此我们需要对 `.NET Framework` 进行详细讨论。

## 8.2 什么是 .NET Framework？

`.NET Framework` 是一种允许在 `Visual Studio` 等集成环境中开发和执行不同应用程序的模型。换句话说，`.NET Framework` 可以被视为使用 C# 或 Visual Basic 等工具和代码开发 Windows 应用、Web 应用或 XML 服务的系统。

`.NET Framework` 的当前版本是 4.8。基本上。.NET Framework 包含以下组件：

- 通用运行时 – `CLR`（称为运行时）。运行时处理语言集成、安全性和内存管理服务。在开发阶段，运行时提供简化开发所需的功能。
- 类库。类库为大多数常见任务（如数据访问、XML 服务和 Windows 表单）提供重用代码。

开发 `.NET Framework` 的主要目标是解决由于不同的客户端浏览器带来的 Web 应用限制。为了解决这些限制，`.NET Framework` 提供了一种与语言和平台无关的通用微软中间语言 (`MSIL`)，并允许任何基于 `.NET` 的语言开发的程序转换为这种 `MSIL`。`MSIL` 可以被通用运行时 (`CLR`) 识别，`CLR` 可以通过本地机器或客户端的即时编译器编译并执行 `MSIL`。

你需要使用 `.NET Framework` 提供的类库访问 `.NET Framework`，并使用 `.NET Framework` 提供的 `Visual Studio` 等工具实现 `.NET Framework`。典型的 `.NET Framework` 模型如图 8.1 所示。`.NET Framework` 支持三种类型的用户界面：

- 运行在 Windows 32 客户端计算机上的 Windows Forms。我们在之前的章节中开发的所有项目都使用了这种用户界面。
- 通过 `ASP.NET` 和超文本传输协议 (`HTTP`) 运行在服务器计算机上的 Web Forms。
- 控制台。

![](img/d59a47501d0a20fc0460a49c469c6fb7_441_0.png)

图 8.1 .NET 框架模型。

总结来说，使用 `.NET Framework` 开发 Windows 端和 Web 应用程序的优势包括但不限于：

- `.NET Framework` 基于 Web 标准，并结合了代码和工程实践，它完全支持 Internet 技术，包括超文本标记语言 (`HTML`)、`HTTP`、`XML`、简单对象访问协议 (`SOAP`)、`XML` 路径语言 (`XPath`) 等其他标准。
- `.NET Framework` 采用统一的应用程序模型设计，因此 `.NET Framework` 提供的任何类的功能都可以被任何 `.NET` 兼容的语言或编程模型使用。同一段代码可以在 Windows 应用程序和 Web 服务中实现。
- `.NET Framework` 对开发者来说易用，因为它被组织成层次化的命名空间和类。`.NET Framework` 提供了一个通用类型系统，称为统一类型系统；它可以被任何 `.NET` 兼容的语言使用。在统一类型系统中，所有语言元素都是对象，可以被任何用任何 `.NET` 语言编写的 `.NET` 应用程序使用。

现在，让我们仔细查看 `ASP.NET`。

## 8.3 什么是 ASP.NET 和 ASP.NET 4.8？

`ASP.NET` 是构建在 `.NET Framework` 之上的编程框架，用于构建 Web 应用程序。在 `.NET Framework` 中开发 `ASP.NET` Web 应用程序与开发 Windows 非常相似。`ASP.NET` Web 应用程序由许多部分和组件组成，但 `ASP.NET` 的核心组件是 `.NET Web Form`（Web 表单）。Web Form 是用户在浏览器中看到的页面，`ASP.NET` Web 应用程序包含一个或多个 Form。

`ASP.NET` 的当前版本是 4.8，它与 `.NET Framework 4.8` 结合，提供了一种专业且方便的方法，帮助用户在 `.NET` 编程语言中构建和开发各种数据驱动的应用程序。随着 `ASP.NET 2.0` 的进展，`ASP.NET 4.8` 的特性是增性的，这意味着从 `.NET Framework` 安装的程序集仍被 4.8 版本使用。简而言之，`ASP.NET 4.8` 没有更改、移除或破坏 2.0 中存在的任何功能、概念或代码，它只是向框架添加了新类型的功能和能力。因此，`ASP.NET 4.8` 是 `ASP.NET 2.0` 的小版本升级；也就是说，`.NET Framework 4.8` 中特定的 `ASP.NET` 新特性相对较少。

## 414 使用 C# SQL Server 数据库编程

### 客户端 ASP.NET Web 服务器

![](img/d59a47501d0a20fc0460a49c469c6fb7_442_0.png)

图 8.2 ASP.NET Web 应用程序的结构。

`ASP.NET 4.8` 中一些值得注意的新特性：

- 核心服务
- 集成 `ASP.NET AJAX`
- Web Forms
- `ASP.NET` 模型-视图控制器 (`MVC`)
- 动态数据
- `ListView` 控制
- `DataPager` 控制

除了这些新特性之外，`ASP.NET 4.8` 和 `ASP.NET 2.0` 之间最重要的区别之一是 `LINQ` 查询被添加到了 `ASP.NET 4.8` 中。`LINQ` 在不同数据库使用的不同查询语法之间提供了一种革命性的解决方案，并弥合了对象世界与数据世界之间的鸿沟。

图 8.2 显示了 `ASP.NET` 应用程序的完整结构。

与可以在客户端运行脚本的传统 Web 页面不同，`ASP.NET` Web Form 还可以运行服务器端代码来访问数据库、创建额外的 Web Forms 或利用服务器的内置安全性。此外，`ASP.NET` Web Form 不依赖于客户端脚本或操作系统。这种独立性允许用户开发单个 Web Form，该表单可以在任何访问互联网并具有 Web 浏览器的设备上查看。

由于 `ASP.NET` 是 `.NET Framework` 的一部分，`ASP.NET` Web 应用程序可以使用任何基于 `.NET` 的语言进行开发。

`ASP.NET` 技术还支持 XML Web 服务。这些是使用 XML 在客户端、应用程序和任何 XML Web 服务之间传输信息的分布式应用程序。

`ASP.NET` Web 应用程序的主要部分包括：

- Web Forms 或 `Default.aspx` 页面。Web Forms 或 `Default.aspx` 页面为 Web 应用程序提供用户界面，这与 Windows 应用程序中的 Web Forms 非常相似。Web Forms 文件以 `.aspx` 扩展名。
- 后代码页面（Code-behind pages）与 Web Forms 相关，包含 Web Form 的服务器端代码。该后代码页面与我们在前面的章节中讨论的 Windows 应用程序中的 Windows Forms 代码窗口非常相似。与 Web Forms 控件相关的大多数事件方法或处理器位于此后代码页面中。后代码页面以 `.aspx.cs` 扩展名标识。
- Web 服务或 asasm Web 页面在创建供其他程序或计算机访问的动态站点时使用。`ASP.NET` Web 服务可能由扩展名为 `.asmx.cs` 设计的后代码页面支持。
- 配置文件。配置文件定义了应用程序的设置。
- `Global.asax`。`Global.asax` 文件用于处理应用程序级事件。
- 缓存（Caching）。缓存允许应用程序存储数据以提高性能。

### 8.3.1 ASP.NET 结构

当运行 `ASP.NET` 应用程序时，会创建以下文件夹：

- `inputroot`。`inputroot` 文件夹包含应用程序的根。
- `bin`。`bin` 文件夹包含编译后的程序集和 DLL 文件。
- `App_Data`。`App_Data` 文件夹用于存储数据文件。
- `App_Code`。`App_Code` 文件夹包含自动编译的源代码。
- `Content`。`Content` 文件夹包含图像、CSS 和 JavaScript 等静态文件。

`ASP.NET` Web 应用程序的主要部分包括：

| 文件夹 | 说明 |
| :--- | :--- |
| inputroot | 应用程序的根，包含页面和静态文件。 |
| bin | 包含编译后的程序集和 DLL 文件。 |
| App_Data | 用于存储本地数据库等数据文件。 |
| App_Code | 包含框架自动编译的源代码。 |
| Content | 包含图像、CSS 和 JavaScript 等静态文件。 |

### 8.3.2 ASP.NET 执行模型

下面的图描述了 `.NET Framework` 的执行模型：

- 程序集文件 (`.dll`)。所有项目被编译成单个程序集文件。
- `AssemblyInfo.cs`。此文件用于写入程序集的通用信息，特别是版本和属性。
- `Global.asax`。`Global.asax` 文件用于处理应用程序级事件。
- 配置（Configuration）。配置文件定义了应用程序的设置。
- 缓存（Caching）。缓存允许应用程序存储数据以提高性能。

当客户端第一次请求 Web 页面时，会发生以下事件：

- 客户端浏览器向服务器获取 GET 请求。
- `ASP.NET` 解析器解释源代码。
- 根据解释结果，如果代码已编译成程序集文件，`ASP.NET` 将请求重定向到相关的程序集文件 (`.dll`)。否则，`ASP.NET` 调用编译器将代码转换为 dll 格式。
- 运行时加载并执行微软中间语言 (`MSIL`) 代码，并向返回所需的 Web 页面。

当用户第二次请求 Web 页面时，不需要编译过程，`ASP.NET` 直接调用 dll 文件并执行 `MSIL` 代码。

### 8.3.3 执行 Web 应用程序时发生了什么？

关键点是 Web Form 是在服务器上构建并运行的。当用户从客户端浏览器发送请求请求该 Web 页面时，服务器需要构建该表单并通过 HTML 格式返回给用户浏览器。一旦客户端浏览器接收到 Web 页面，客户端与服务器之间的连接就会终止。

为了让这个问题更加清晰，我们可以用登录表单为例。当用户第一次向服务器发送请求启动登录流程时，服务器构建登录表单并以 HTML 格式将其发送回客户端。之后，客户端与服务器之间的连接会被保存。当用户接收到登录 Web页面并输入必要的登录信息（如用户名和密码）后，用户需要向服务器发送另一个请求来处理这些登录信息。服务器接收并处理登录后，如果发现信息无效，服务器则需要重新构建登录表单，并将某些警告消息发送回客户端。因此，你可以看到在 Web 应用程序执行过程中，客户端和服务器之间发生了多少次往返（round trips）。

减少往返的良好解决方案是确保来自客户端的所有信息尽可能准确。换句话说，尽量在客户端进行任何验证，以减轻服务器的负担。

现在，我们已经完成了关于 `.NET Framework`、`ASP.NET` 以及 `ASP.NET` Web 应用程序的讨论。我们将使用 `ASP.NET` Web Forms 创建并开发一些 Web 项目，以说明如何通过 Web 浏览器访问数据库，并在网页上进行选择、显示和操作。

### 8.3.4 测试和运行 Web 项目的要求

开始使用 `ASP.NET` 创建真实的 Web 项目之前，我们需要以下要求来测试和运行我们的项目：

- 1) 服务器：为了测试和运行我们的项目，你需要在本地计算机或网络上有一个 Web 服务器。默认情况下，如果你在本地计算机上安装了 `Visual Studio 2022 Community`，本地计算机上已经安装了 `IIS 10.0`。此软件允许你的 Web 开发工具使用 `Visual.NET` 连接到服务器，以便从服务器上传或下载页面。
- 2) 在此，为了让我们的真实 Web 项目简单易用，我们始终使用本地计算机作为伪服务器。换句话说，我们始终使用 `localhost`（本地计算机的 IP 名称）作为我们的 Web 服务器与浏览器通信，执行数据访问和操作。

如果你没有在计算机上启用 `IIS`，请按照以下步骤在计算机上启用此组件：

- 点击“开始”，然后点击“控制面板”，点击“程序”。
- 在“程序和功能”项下，点击“启用或关闭 Windows 功能”链接以打开功能向导，如图 8.4 所示。
- 从列表中勾选“Internet 信息服务”项的复选框以启用计算机上的 `IIS`。
- 要确认此启用功能，展开“Internet 信息服务”项，并确保“Web 管理工具”和“万维网服务”这两个项也已启用。这可以通过两个复选框上的选择标记来指示，如图 8.4 所示。
- 点击“确定”按钮激活此 `IIS` 并关闭功能向导。
- 激活将在下一个向导开始启用此 `IIS`，完成后将显示完成消息。只需点击“关闭”按钮即可完成此启用过程。最后关闭控制面板。

你可能需要重启计算机以使启用功能生效。

![](img/d59a47501d0a20fc0460a49c469c6fb7_446_0.png)

图 8.4 打开的 Windows 功能向导。

如你所知，`.NET Framework` 包含了两个访问企业数据库的数据提供程序：用于 OLE DB 的 `.NET Framework Data Provider` 和用于 SQL Server 的 `.NET Framework Data Provider`。由于 Microsoft Access 数据库与 SQL Server 数据库没有太大，在本章中，我们将使用 SQL Server 作为目标数据库，说明如何通过 Web 浏览器访问数据库，并在网页上进行选择、显示和操作。

- 1) 开发 `ASP.NET` 以选择和显示。
- 2) 开发 `ASP.NET` 以选择和插入。
- 3) 开发 `ASP.NET` 以选择和更新。
- 4) 开发 `ASP.NET` 以选择和删除。

让我们开始使用 `ASP.NET` 创建登录项目。然而，在开始之前，我们需要以下内容：

### 8.3.5 安装缺失的组件

- 1) 打开模板。
- 2) 进入菜单。
- 3) 打开向导。
- 4) 向下滚动到 the..
 5) the the..
   )) the.
  7) the the.

## 8.4 创建 Web应用程序从数据库选择数据

- 1) 打开模板。
- 2) 进入菜单。
- 3) 打开向导。
- 4) 进入项目。
- 5) 保存项目。
- 6) 点击按钮。

- 1) 打开项目。
- 2) 打开项目。
- 3) 打开项目。
- 4) The the the the the the is to is in the code.

需要注意的是代码中的代码行：`<form id="form1" runat="server">`。此行代码表示该 Web 表单将在页面开始时在服务器上运行。

让我们从解决方案（Solution Explorer）查看视图设计器（View Designer），以打开 Web 表单的设计视图。

![](img/d59a47501d0a20fc0460a49c469c6fb7_447_0.png)

图 8.5 打开的模板。

### 4.4.1 创建用户界面

右键点击 **Default** 项并从弹出菜单中选择 **Rename**（重命名），并将 Web Form 的名称改为 **Login.aspx**，因为我们希望将此默认项作为登录页面。

![](img/d59a47501d0a20fc0460a49c469c6fb7_448_0.png)

图 8.4 选中的 Web 表单。

| 类型 | ID | Text | TabIndex | BackColor | TextMode | Font |
|---|---|---|---|---|---|---|
| Label | Label1 | 欢迎来到 CSE 系 | 0 | #E0E0E0 | | 粗/大号 |
| Label | Label2 | 用户名 | 1 | | | 粗/小号 |
| Textbox | txtUserName | | 2 | | | |
| Label | Label3 | 密码 | 3 | | | 粗/小号 |
| Textbox | txtPassWord | | 4 | | Password | |
| Button | cmdLogin | 登录 | 5 | | | 粗/中 |
| Button | cmdCancel | 取消 | 6 | | | 粗/中 |

**图 8.7** 登录表单的控件。

与 Windows 表单的另一个不同在于，当你将这些控件添加到 Web 表单时，你必须首先在 Web 表单中使用键盘上的 **Space** 键找到要添加控件的位置，然后从工具箱窗口选取一个控件并将其拖到该位置。你不能像在 Web 表单中那样随地选择或拖动控件到随机位置，这是 Windows 表单与 Web 表单之间的显著区别。

不过，一个例外或好消息是，对于 `Visual Studio 2022`，只要你将每个控件的 **Position** 属性设置为 **Absolute**（绝对），你就可以像在 Windows Form 中一样添加并将任何控件放在任何随机位置。要这样做，需要：

- 1. 在 Web 表单的某个位置添加控件。
2. 点击选中该控件。
3. 进入 **Format | Set Position** 菜单项并勾选 **Absolute** 属性。

完成此设置后，你可以随心移动移动任何控件到任何随机位置，这大大提高了我们构建 Web 表单的灵活性和效率。
你完成的用户界面应该如图 8.8 所示。

![](img/d59a47501d0a20fc0460a49c469c6fb7_449_0.png)

**图 8.8** 完成的登录 Web 表单。

在我们将代码添加到后置页面（code-behind page）以重命名控件并执行登录过程之前，必须先运行项目，允许 `Web.config` 文件识别我们已添加到 Web 表单中的那些控件。点击工具栏上运行我们项目的 `IIS Express` 按钮。我们可能需要点击两个提示对话框中的“是”，以便我们的 Web 页面获得证书并被本地服务器识别。运行的 Web 页面应该与图 8.8 一致。点击表单右上角的 Close 按钮以完成此阶段。

- 将控件添加到 Web 表单随机位置的一个重要且有趣的点是，将每个控件的 Position 属性设置为 Absolute 值。在完成此设置后，你可以像操作 Windows Form 那样添加任何控件并将其移动到任何位置。

现在编写访问数据库以执行登录过程的代码。

### 8.4.2 开发代码以访问和从数据库选择数据

通过右键点击 `Login.aspx` 并在解决方案管理器中选择 View Code（查看代码）按钮来打开后置页面。首先，我们需要像在之前的章节的项目中所做的那样添加一个 SQL Server 数据相关的命名空间。将以下命名空间添加到此代码窗口的顶部，以引入数据库和 SQL Server 数据提供程序所需的命名空间：

```csharp
```
