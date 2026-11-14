

这是一个非常实用的包，它为开发者提供了一种新的应用程序类型，可通过 dotnet CLI 生成，它还提供了创建新小部件、窗口或对话框对象的可能性（包含 .glade 文件）。

模板包的安装可以使用下面描述的命令行完成（这是安装 dotnet CLI 新项目模板的标准命令行）：

```
C:>dotnet new install
GtkSharp.Template.CSharp --version
3.22.24.37
```

版本号是可选的，可以省略。以下是安装此模板包后的结果屏幕（图 1）。

![](img/3d310cc066dda6e2dfa67a650614076f_196_0.png)

(图 1)

安装此包后，GTK 新项目模板应可通过“dotnet new”命令行使用，这些新项目包括：

- GtkSharp.Application: 生成一个完整的 Gtk 应用程序，包含 .csproj、.cs 和 glade 文件。
- GtkSharp.Dialog: 生成 .cs/.glade 文件，用于向现有项目添加对话框窗口。
- GtkSharp.Widget: 为控件（小部件）生成 .cs/.glade 文件。
- GtkSharp.Window: 生成基本 gtk.window 的 .cs/.glade 文件。

只有 GtkSharp.Application 是 .NET Core 的项目模板，其他的是用于向应用程序添加元素（对话框、小部件、窗口）的项模板，生成元素的默认名称是执行命令的文件夹名称（如果未指定输出名称）。

您可以使用命令“dotnet --list”验证所有这些模板是否已正确安装，该命令列出“dotnet new”命令的可用模板，如下所示。

```
C:>dotnet new --list -lang C#
```

“-lang”选项用作结果过滤器，仅选择 C# 类型的项目。此命令的结果如下：

| 短名称 | 语言 | 标签 |
| :--- | :--- | :--- |
| 控制台应用程序 | console | C#, C++, F#, VB |
| 类库 | classlib | C#, C++, F#, VB |
| 单元测试项目 | unittest | C#, C++, F#, VB |
| xUnit 测试项目 | xunit | C#, C++, F#, VB |
| ASP.NET Core 空应用 | web | C# |
| ASP.NET Core Web 应用 (模型-视图-控制器) | mvc | C#, F# |
| ASP.NET Core Web 应用 | razor | C# |
| ASP.NET Core 与 Angular | angular | C# |
| ASP.NET Core 与 React.js | react | C# |
| ASP.NET Core 与 React.js 和 Redux | reactredux | C# |
| Razor 类库 | razorclasslib | C# |
| Razor 页面 | page | C# |
| Microsoft Identity Platform (Azure AD v2.0) Web 应用程序 | webapp | C# |
| 辅助角色服务 | worker | C# |
| gRPC 服务 | grpc | C# |

您现在可以使用 .NET Core 3 命令行客户端创建新的 GTK 应用程序，如下所示：

```
C:>dotnet new gtkapp -n sampleGtkApp
```

此命令行将创建名为“sampleGtkApp”的 GTK 应用程序项目（这是新 dotnet CLI 命令的标准行为）。

创建的模板应用程序使用 .glade 文件格式来描述 GUI。此格式可以加载到 Gtk.Builder 对象中（我们将在后面详细介绍此点）。

您可以通过以下参考链接了解有关使用 Gtk.Builder 的更多信息。

```
http://gtkbuilder.org/
http://gnome.org/gtkbuilder
```

在模板中，.cs 文件和 .glade 文件同名，这使开发者可以轻松修改窗口的两个方面（前端和后端）。

生成的应用程序可以轻松修改和扩展；通过使用 Glade 编辑对应主窗口的 XML 文件（.glade 扩展名）。

您可以注意到，此包生成的应用程序模板使用基于 XML 文件的 GUI 模型。但使用 GTK，您也可以使用内联 C# 代码实现 GUI，我们将在示例部分回顾这两种 GTK 实现类型。

在继续之前，有必要研究 GTK 界面设计器：Glade。

## 8.5.4 Glade：用户界面设计器

Glade 是一个允许在不手动编写代码的情况下构思和设计 GUI 的应用程序。此应用程序取代了 Stetic GUI 设计器（用于 Mono，跨平台 .NET 框架）。

与其前身一样，它是一个具有 WYSIWYG 功能的 RAD 工具，可轻松开发 GTK+ GUI。Glade 与编程语言无关，这意味着它不生成任何代码，描述所设计 GUI 的文件按照标准 XML 格式编码。GTKBuilder 是此 XML 文件的格式。

Glade 负责生成描述 UI 的 XML 代码，并生成可通过 GtkBuilder（使用 GtkBuilder 对象）加载的 XML 文件。此后，这些 XML 文件可用于您的 GTK# .NET Core 3 C# 应用程序（实际上适用于您用于使用 GTK 工具包开发的任何语言）。

您可以通过以下参考链接了解有关 Glade 的更多信息。

![](img/3d310cc066dda6e2dfa67a650614076f_200_0.png)

### 8.5.4.1 为 Visual Studio 2019 安装 Glade 以供使用

为了方便编辑 GUI XML 文件，可以从 Visual Studio 2019 内部调用 Glade。

您可以在 Visual Studio 中轻松将 Glade 配置为打开“.glade”扩展名文件类型的默认程序（图 1）。因此，GTK GUI 的集成将显示为集成在 Visual Studio 环境中，您将能够从 Visual Studio 的“解决方案资源管理器”中编辑“.glade”文件。

![](img/3d310cc066dda6e2dfa67a650614076f_201_0.png)

(图 1)

打开“glade”文件时，必须选择“设置为默认”，以便与 Glade 建立永久关联。

在 Visual Studio 中完成 Glade 的安装和配置后，您只需在“解决方案资源管理器”视图中双击它，即可根据要求编辑“glade”文件。

### 8.5.4.2 使用 Glade 进行界面设计

使用 Glade 设计 GUI 对每个开发者来说几乎都是直观的（几乎与 Visual Studio 中的 Winforms 设计器相同）。如下（图 2）所示，它提供类似的功能。

![](img/3d310cc066dda6e2dfa67a650614076f_202_0.png)

(图 2)

Glade 应用程序（图 2）由三个不同的面板组成，对应应用程序的三个功能：

- 左侧面板：表示容器中存在的小部件的层级树。Glade 允许添加小部件或容器（对于 GTK 来说，容器也是一种小部件）。表单（或屏幕）设计遵循小部件的层级树。您也可以在此视图中按名称选择小部件。
- 中间面板：设计器的主视图。此面板允许开发者设置所选小部件的位置和大小（它也允许小部件选择）以及添加新小部件。
- 右侧面板：此面板根据所选选项卡汇集四个不同的功能：
  1. 所选小部件属性的视图（带有“常规”选项卡）。
  2. 用于小部件定位及其在 GTK 术语中的停靠和打包的视图（带有“打包”选项卡）。
  3. 用于当前所选小部件常用属性的视图（带有“常用”选项卡）。
  4. 用于管理与小部件关联的不同事件上发送的信号的视图（带有“信号”选项卡）。

这些简单概念足以使用 Glade 为您的应用程序设计高效的 GUI。

请注意，掌握 Glade 并非立即可行，应该需要一个学习曲线，因开发者而异。

### 8.5.4.3 在 Glade 中定义信号/处理程序

完成图形设计后，可以使用 Glade 在界面和后端程序（C# 代码）之间建立链接。

GTK 遵循信号/处理程序类型的架构（一种经典架构）。根据此逻辑，Glade 允许开发者指定特定小部件上事件发送的信号类型（在右侧面板中）。此实现直接从 Glade 应用程序完成，即通过在特定信号上指定适当的方法名称调用，如所述（图 3）。

您会注意到 Glade 界面中某些信号标记为“已弃用”，但您也可以使用已弃用的信号（如屏幕截图所示）。

