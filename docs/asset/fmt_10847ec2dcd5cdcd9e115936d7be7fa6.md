
- 提高了对 IPv6 的支持。

### WPF 的改进

.NET Framework 4.5 为 WPF 提供了以下改进：

- 包含新的 Ribbon 控件用于实现具有快速访问栏、应用程序菜单和标签页的 UI。
- 新的 `INotifyDataErrorInfo` 接口支持同步和异步数据验证。
- `VirtualizingPanel` 和 `Dispatcher` 类包含新功能。
- 在显示大型分组数据集和在非 UI 线程上检索集合时提供了更好的性能。

# C# .NET 基础

- 提供了与静态属性的数据绑定、到实现 `ICustomProvider` 接口的自定义类型的数据绑定，以及从绑定表达式获取数据绑定信息的功能。
- 提供了值更改时重新定位数据查看器的功能，也称为动态塑形（live shaping）。
- 提供了检查项目内容数据是否已断开的功能。
- 提供了固定属性更改与数据源更新之间应消耗的时间的功能。
- 提供了实现 Web 事件（we-event）模式的支持。此外，事件现在能够支持标记扩展。

# WCF 的改进

.NET Framework 4.5 提供了以下新功能和增强，使 WCF 应用程序的开发和维护更加简单。

- 简化生成的配置文件。
- 提供了对合约优先（contract-first）开发的支持。
- 提供了在 ASP.NET 兼容模式下更易地调试传输属性的能力。
- 包含了 `XmlReaderQuotas` 类中的增强，以减少 XML 字典读取器显式设置这些值的可能性。
- 在应用程序的生成过程中验证 WCF 配置文件，以便您可以在执行应用程序之前检测到配置错误。
- 提供了对新的异步流的支持。
- 包含了安全超文本传输协议 (HTTPS) 协议映射，以增加通过 IIS 在 HTTPS 上暴露端点的可见度。
- 提供了通过在服务 URL 末尾附加 `singleWSDL` 在单个 WSDL 文档中生成元数据的能力。
- 支持 WebSockets，允许通过 80 和 443 端口进行双向通信，其性能特性等同于 TCP 传输。
- 提供了在代码中配置服务的支持。
- 提供了 XML 编辑器提示。
- 提供了对 `ChannelFactory` 缓存的支持。
- 提供了对用户数据报协议 (UDP) 传输的支持，允许您创建使用“发后即忘”消息的服务。在类服务中，客户端向服务发送消息，而不期望服务的任何响应。
- 提供了在单个 WCF 端点上使用 HTTP 传输和安全的同时支持多种认证模式的能力。
- 提供了对使用国际化域名的 WCF 服务的支持。

# WF 的改进

.NET Framework 4.5 包含了 WF 中的新功能，如下：

- 状态机工作流包含了若干新类和活动中的增强，如下：
  - 提供了在状态上设置断点的功能
  - 提供了在工作流设计器中复制和粘贴转换的功能
  - 支持创建共享触发器转换工作流，包括 `StateMachine`、`State` 和 `Transition`

## 第 1 章

工作流设计器功能的增强如下：

- 包含了如快速查找（Quick Find）和在文件中查找（Find in Files）等功能。
- 当向容器活动添加第二个子活动时，会自动创建一个序列（Sequence）活动以包含该子活动和一个容器活动。
- 支持平移，允许在不使用滚动条的情况下修改工作流的可视部分。
- 包含一个新的文档输出（Document Output）视图，以树状大纲视图显示工作流的组件，并允许您从文档输出视图选择组件。
- 提供了为工作流添加注释的能力。
- 提供了使用工作流设计器定义和消费活动委托的能力。
- 包含了状态机和流程图中活动及转换的如自动连接（Auto-connect）和自动插入（Auto-insert）等属性。
- 包含了在工作流 XAML 文件的单个元素中存储状态信息的能力，以便您可以轻松地查找和操作状态信息。
- 包含了 `NoPersistScope` 以防止子活动的持久化。
- 工作流项目对如 C# 和 VB 等语言的表达式提供以下支持：
  - 在 VB 中开发的工作流项目将使用 VB 表达式；同样地，C# 工作流项目将使用 C# 表达式。
  - 在 Visual Studio 2010 中开发的包含 VB 表达式的 C# 项目与包含 C# 表达式的 C# 工作流项目具有兼容性。
- 支持版本控制方面的增强：
  - 包含了 `WorkflowClass`，它提供了持久化实例与其定义之间的映射。
  - 支持在同一宿主机中运行多个工作流定义。
  - 提供了对持久化实例定义的增强。
- 在应用程序的生成过程中验证 WCF 配置文件，以便您可以在执行应用程序之前检测到配置错误。

工作流设计器各项功能的增强如下：

- 包含了如快速查找和在文件中查找等功能。
- 当向容器活动添加第二个子活动时，会自动创建一个序列活动来包含这些活动。
- 支持平移，允许在不使用滚动条的情况下修改工作流的可视部分。
- 包含一个新的文档输出视图，以树状大纲视图显示工作流的组件，并允许您从文档输出视图选择组件。
- 提供了为工作流添加注释的能力。
- 提供了使用工作流设计器定义和消费活动委托的能力。
- 包含了状态机和流程图中活动及转换的如自动连接和自动插入等属性。
- 包含了在工作流 XAML 文件的单个元素中存储状态信息的能力，以便您可以轻松地查找和操作状态信息。
- 包含了 `NoPersistScope` 以防止子活动的持久化。
- 工作流项目对如 C# 和 VB 等语言的表达式提供以下支持：
  - 在 VB 中开发的工作流项目将使用 VB 表达式；同样地，C# 工作流项目将使用 C# 表达式。
  - 在 Visual Studio 2010 中开发的包含 VB 表达式的 C# 项目与包含 C# 表达式的 C# 工作流项目具有兼容性。
- 支持版本控制方面的增强：
  - 包含了 `WorkflowClass`，它提供了持久化实例与其定义之间的映射。
  - 支持在同一宿主机中运行多个工作流定义。
  - 提供了对持久化实例定义的增强。

让我们在应用程序生成过程中验证 WCF 配置文件，以便您可以在执行应用程序之前检测到配置错误。

让我们进入 Visual Studio 2012。Visual Studio 2012 是一个用于编写、编译和调试代码的 IDE，比之前的版本要容易得多。它包含了一套完整的工具，用于构建 ASP.NET 应用程序、Web 服务、桌面应用程序和移动应用程序。

## 第二部分：Visual Studio 2012 简介

Visual Studio 是微软提供的集成开发环境（IDE），用于创建 Windows、Web 以及移动应用程序，支持 Visual Basic、C# 和 C++ 等语言。早期的，在旧版本的 Visual Studio 中创建的项目在新版本的 Visual Studio 中打开时，Visual Studio 会执行转换向导，将项目升级到新版本。转换后，项目无法在源自的旧版本中打开。后兼容性在 Visual Studio 2012 中有所提高。这意味着转换后，Visual Studio 2010 项目既可以在 Visual Studio 2012 中打开，也可以在 Visual Studio 2010 中打开。这是通过在转换后的文件中添加一些后兼容性属性实现的，如下：

# .NET 基础

- 支持多个版本的 .NET
- 数据检索和绑定的增强
- 检查需要重构的代码
- 与 .NET Framework 4.5 集成
- 简化设计过程

现在，让我们探索 Visual Studio 2012 及其新功能。

# Visual Studio 2012 的新功能

- 项目兼容性
- ASP.NET 4.5 网站模板
- Internet 信息服务 (IIS) 7.5 原生支持
- 超文本标记语言 (HTML) 编辑器
- JavaScript 编辑器
- 层级样式表 (CSS) 编辑器
- 页面检查工具
- 发布
- 开发 Windows 应用的支持
- 增强云能力
- 启动页的新标签
- 应用生命周期管理 (ALM) 和 基础程序服务器 (TFS)
- 管理应用生命周期
- 建模
- 应用应用以及团队协作
- 构建自动化和调试
- Microsoft 测试管理器

让我们详细了解这些内容。

## 项目兼容性

早期，当旧版本 Visual Studio 中创建的项目在新版本 Visual Studio 中打开时，Visual Studio 会自动执行转换向导，将项目升级并转换为新版本。转换后，项目无法在源自的旧版本中打开。后兼容性在 Visual Studio 2012 中有所提高。这意味着转换后，Visual Studio 2010 项目既可以在 Visual Studio 2012 中打开，也可以在 Visual Studio 2010 中打开。这是通过在 Visual Studio 2012 中转换后的文件中添加一些后兼容性属性实现的，如下：

## 第1章

此外，您应该更改导入元素以保持与不同版本 Visual Studio 的兼容。请注意，如果项目在两台不同电脑的 Visual Studio 2010 和 Visual Studio 2012 之间共享，并在 .Data 文件中使用了本地数据库，则两台电脑上必须安装相同名称的 SQL Server。

## ASP.NET网站模板中的配置更改

Visual Studio 2012 对默认的 Web.config 文件引入了一些更改，用于使用 ASP.NET 网站模板配置 ASP.NET 网站。以下是 ASP.NET 网站中的配置更改：

- `<httpRuntime>` 元素的 `encoderType` 属性被设置为默认值 `AutoEncoder`，以包含编码程序。这些编码程序增加了 AntiXSS 库的普及。这些编码程序存在 System.Web.AntiXSS 命名空间中。你可以通过让它运行或在 Web.config 文件中配置它来使用 `AutoEncoder` 类。当你将 `encoderType` 属性设置为 `AutoEncoder` 时，ASP.NET 中的所有输出编码器默认将使用新的编码程序。
- `<httpRuntime>` 元素的 `validationMode` 属性被设置为默认值 `4.5`，这表示对请求进行延迟或懒性验证。相比之下，之前的 ASP.NET 版本默认会对潜在的跨站脚本攻击进行验证，如果某些请求在标头或 Cookie 中查找标记，则会抛出异常。ASP.NET 4.5 引入了两个允许处理未评估数据的功能。这些功能是延迟或懒性验证以及对未评估数据的访问。
- `<system.webserver>` 部分的 `<modules>` 元素中删除了 `RunManagedModulesForAllRequests` 属性。然而，删除 `RunManagedModulesForAllRequests` 可能会在引入和生成程序时导致某些问题。

## IIS 7.5 用于 ASP.NET 路由的原生 HTTP

Visual Studio 2012 引入了用于 ASP.NET 路由的原生 IIS 7.5。在 Visual Studio 2012 模板更改之前，Web.config 配置支持路由，如图1.8所示：

```xml
<xml version="1.0"?>
<configuration>
  <system.web>
    <modules runManagedModulesForAllRequests="true">
      <!-- some code -->
    </modules>
  </system.web>
  <system.webserver>
</configuration>
```

图1.8：显示 ASP.NET 路由的 Web.config 文件

如图1.8所示，`RunManagedModulesForAllRequests` 属性被设置为 `true`；但为请求增加了不必要的开销。该属性在 ASP.NET 4.5 中被删除，这意味着该设置是默认的。如果你使用没有 Service Pack 1 的 Windows 7，路由期间可能会发生错误。在这种情况下，你需要手动将 `RunManagedModulesForAllRequests` 属性设置为 `true`，但会产生一些开销。

## HTML 编辑器

Visual Studio 2012 在 HTML 编辑器中引入了新功能，帮助程序员完成任务。HTML 编辑器中添加的新功能包括：

- 智能任务 (Smart Tasks) - 当插入点位于服务器元素内部时，添加一个小小的符号来连接服务器标签。点击该符号或从键盘按下 `Ctrl +` 组合键时，会显示智能任务。智能任务在之前的 Visual Studio 版本中已经可用，但可以通过设计视图使用。然而，在 Visual Studio 2012 中，也可以源代码视图中使用智能任务。图1.9 显示了源代码视图中与 Calendar 标签相关的智能任务菜单：

26

# C#.NET 基础

![](img/17af790174c480761404624aeed9b30b_66_0.png)

图1.9：在源代码视图中显示智能任务

在图1.9 中，智能任务选择了 `Calendar Tasks` 选项，如 `Form Element` 和 `Auto Format`。从右键菜单中选择一个选项将显示与其相关的任务。例如，如果你选择 `Auto Format` 选项，就会出现 `AutoFormat` 对话框，如图1.10所示。

![](img/17af790174c480761404624aeed9b30b_66_1.png)

图1.10：利用 AutoFormat 对话框

你可以在对话框中选择任何你喜欢的设置，例如，你可以从对话框左侧面板的 Select schema 列表框中选择 `Simple` 选项并点击 OK 按钮。所选方案的代码片段将出现在包含该标签（例如，Calendar 标签）的代码中。图1.11 显示了应用的片段：

```xml
<asp:Calendar id="calendar1" runat="server" BorderColor="#999999" CellPadding="Shortest"
Font-Name="Arial" Font-Size="" ForeColor="Black" Height="100%" Width="200px">
<DayHeaderStyle VerticalAlignment="Center" BackColor="#CCCCCC" /></NextDayHeaderStyle>
<OtherMonthDayStyle BackColor="#F0F0F0" /></OtherMonthDayStyle>
<SelectedDayStyle BackColor="#CCCCCC" Font-Bold="True" ForeColor="white" /></SelectedDayStyle>
<SelectorStyle BackColor="#CCCCCC" /></SelectorStyle>
<TitleStyle BackColor="#999999" Font-Bold="True" /></TitleStyle>
<TodayDayStyle BackColor="#FFFF00" /></TodayDayStyle>
<WeekendDayStyle BackColor="#FFFF00" /></WeekendDayStyle>
</asp:Calendar>
```

WAI-ARIA - Web可访问性增强 - 丰富的互联网应用程序。在 Visual Studio 2012 中引入是为了使网站可访问。WAI-ARIA 规范定义了 `div` 元素的属性，用于创建弹出窗口。WAI-ARIA 规范定义了 `div` 元素的属性，用于创建弹出窗口。

27

## 第1章

```xml
<div aria-descendant
  aria-autocomplete
  aria-busy
  aria-checked
  aria-describedby
  aria-disabled
  aria-controls
</div>
```

图1.12：显示 属性列表

你可以从图1.12所示的列表中选择任何 aria-属性；在我们的案例中，我们选择了。之后，会出现另一个列表包含：

```xml
  execute
  grab
  move
  popup
</div>
```

图1.13：显示 Aria 属性的值

- 新 HTML 5 代码片段 - 指一种添加了可以根据编程需求自定义的5 标记的功能。这些代码片段使程序员的工作更简单、更快。要调用任何 HTML 元素的代码片段，你需要在从智能提示选择元素后按下 Tab 键。例如，从智能提示中选择了 `<video>` 元素，如图1.14所示：

```xml
<div
  <video src="file.mp4" type="video/mp4">
  <source src="file.webm" type="video/webm">
  <source src="file.ogg" type="video/ogg">
</video>
</div>
```

图1.14：用于选择 <video> 元素的智能提示

当你在选择 `<video>` 元素后按下 Tab 键时，会出现该元素的对应代码片段，如图1.15所示：

```xml
<div
  <video controls="controls">
  <source src="file.mp4" type="video/mp4">
  <source src="file.webm" type="video/webm">
  <source src="file.ogg" type="video/ogg">
</video>
</div>
```

图1.15：显示自动生成的代码

- 提取用户控件 - 允许程序员将 Web 页面内容的各个部分组合成逻辑单元，例如用户控件。这有助于重构代码、增加页面的可读性并简化页面结构。要在源代码视图中使用 Web Forms，选择可以移动到用户控件的文本，然后右键点击选中的文本打开右键菜单。进一步，从右键菜单中选择“提取到用户控件”选项，如图1.16所示：

28
