
表 1-3 描述了你在 ASP.NET 4 中可用的指令。

# 表 1-3

| 指令 (DIRECTIVE) | 描述 |
|---|---|
| Assembly | 链接到与其关联的页面或用户控件。 |
| Control | 用于用户控件 (.ascx) 的页面指令。 |
| Implements | 实现指定的 .NET Framework 接口。 |
| Import | 将命名空间导入到页面或用户控件。 |
| Master | 允许你在页面解析或编译时指定用于主页特定的属性和值。此指令只能与主页 (.master) 使用。 |
| MasterType | 将类名与页面关联，以获取包含在指定主页中的强类型引用或成员。 |
| OutputCache | 控制页面或用户控件的缓存策略。 |
| Page | 允许你在页面解析或编译时指定用于页面特定的属性和值。此指令只能与 ASP.NET 页面 (.aspx) 使用。 |
| PreviousPageType | 允许 ASP.NET 页面处理来自应用程序中另一个页面的回传（postback）。 |
| Reference | 将页面或用户控件链接到当前页面或用户控件。 |
| Register | 将别名与命名空间和类名关联，以便在自定义服务器控件语法中使用。 |

## @Page

接下来的章节对这些指令中的每一个进行了快速复习。
`@Page` 指令允许你为 ASP.NET 页面 (.aspx) 指定属性和值，以便在页面解析或编译时使用。它是这一组中最频繁使用的指令。ASP.NET 页面是 ASP.NET 如此重要的部分，你有许多属性可以使用。

表 1-4 总结了通过 `@Page` 指令可用的属性。

# 表 1-4

| 属性 (ATTRIBUTE) | 描述 |
|---|---|
| AspCompat | 当赋值为 True 时，允许页面在单线程表象上执行。该属性的默认设置为 False。 |
| Async | 指定 ASP.NET 页面是同步还是异步处理的。 |
| AsyncTimeout | 指定等待异步任务完成的数（秒为单位）。默认设置为 45 秒。 |
| AutoEventWireup | 指定当设置为 True 时，页面事件是否是自动化的。该属性的默认设置为 True。 |
| Buffer | 当设置为 True 时，启用 HTTP 响应缓冲。该属性的默认设置为 True。 |
| ClassName | 指定页面编译时绑定到页面的类名称。 |

## ASP.NET 4 页面指令

| 属性 (ATTRIBUTE) | 描述 |
|---|---|
| ClientIDMode | 指定页面在生成页面上控件的 ClientID 值时使用的算法。默认值为 AutoID（ASP.NET 4 之前使用的模式）。这是 ASP.NET 4 的一个新属性。 |
| ClientTarget | 指定控件渲染程序的目标代理。此属性需要绑定到 web.config 文件中 `<clientTarget>` 部分定义。 |
| CodeFile | 引用与页面关联的代码后文件。 |
| CodeFileBaseClass | 指定与代码后类一起使用的基类类型名称，由 CodeFile 属性使用。 |
| CodePage | 指明响应的代码页值。 |
| CompilationMode | 指定 ASP.NET 是否应该编译页面。可用选项包括 Always（默认）、Auto 或 Never。设置为 Auto 意味着如果可能，ASP.NET 将不编译页面。 |
| CompilerOptions | 包含页面编译选项的编译器字符串。 |
| CompileWith | 指向代码后文件的字符串值。 |
| ContentType | 定义响应的 HTTP 内容 MIME 类型。 |
| Culture | 指定页面的设置。ASP.NET 3.5 和 4 允许将 Culture 属性赋予 Auto 以启用自动检测文化。 |
| Debug |设置为 True 时使用调试符号编译页面。 |
| Description | 提供页面的文本描述。ASP.NET 忽略此属性及其赋值。 |
| EnableEventValidation | 指定在回传和回调场景下启用事件验证。默认设置为 True 意味着将对事件验证。 |
| EnableSessionState | 设置为 True 时启用页面会话状态。该属性的默认设置为 True。 |
| EnableTheming | 设置为 True 时启用页面使用主题。该属性的默认设置为 True。 |
| EnableViewState | 设置为 True 时跨页面维护视图状态。默认值为 True。 |
| EnableViewStateMac | 当页面从用户处回传时，对页面视图状态运行机器身份验证检查（设置为 True）。默认值为 False。 |
| ErrorPage | 指定用于处理所有未处理异常的 URL。 |
| Explicit | 设置为 True 时启用 Visual Basic 选项。默认设置为 False。 |
| Language | 定义任何内联渲染和脚本块使用的语言。 |
| LCID | 定义 Web 页面的本地标识符。 |
| LinePragmas | 布尔值，指定在生成的程序集中是否使用行指令。 |
| MasterFilePath | 指向与页面一起使用的主页位置的字符串值。此属性用于内容页面。 |
| MaintainScrollPosition | 取决于布尔值，表示页面应保持在相同的滚动位置，还是在页面向自身回传时重新生成在顶部位置。 |
| Postback | |

# 第一章 应用程序页面框架

表 1-4（续）

| 属性 | 说明 |
| --- | --- |
| MetaDescription | 允许你在 meta 标签中指定用于 SEO 目的的描述信息。这是 ASP.NET 4 中的一个新属性。 |
| MetaKeywords | 允许你在 meta 标签中指定用于 SEO 目的的关键字。这是 ASP.NET 4 中的一个新属性。 |
| ResponseEncoding | 指定页面内容的编码。 |
| SmartNavigation | 指定是否为功能更丰富的浏览器激活 ASP.NET 智能导航功能。它会将焦点返回到页面的当前位置。默认值为 False。从 ASP.NET 2.0 开始，SmartNavigation 已被弃用。请使用 `Focus()` 方法和 `MaintainScrollPositionOnPostback` 属性。 |
| Src | 指向用于渲染的页面后台代码（code behind）的类源文件。 |
| Strict | 设置为 True 时，使用 Visual Basic 模式编译页面。默认设置为 False。 |
| StylesheetTheme | 使用 ASP.NET 特性将指定的主应用于页面。StylesheetTheme 和 Theme 属性的区别在于，StylesheetTheme 不会覆盖控件中已有的主题，而 Theme 会移除这些主题。 |
| Theme | 使用 ASP.NET 将指定的主应用于页面。 |
| Title | 应用页面的标题。此属性主要用于内容页面，这些页面必须应用不同于主页中指定的页面标题。 |
| Trace | 设置为 True 时启用页面跟踪。默认设置为 False。 |
| TraceMode | 指定在启用跟踪时跟踪消息的显示方式。此属性的设置包括 SortByType 或 SortByCategory。默认设置为 SortByType。 |
| Transaction | 指定页面上是否支持事务。此属性的设置有 Disabled、NotSupported、Required 和 RequiresNew。默认设置为 Disabled。 |
| UICulture | Culture 属性的值指定了 ASP.NET 页面使用的 UI 语言（界面文化）。ASP.NET 3.5 和 4 包含了将 Culture 属性值设置为 Auto 的功能，以启用 UI 的自动检测。 |
| ValidateRequest | 设置为 True 时，将对表单输入值与潜在危险值列表进行检查。这可以保护你的 Web 应用程序免受 JavaScript 攻击等有害攻击。默认是 True。 |
| ViewStateEncryptionMode | 指定页面上加密 ViewState 的方式。选项包括 Auto、Always 和 Never。默认是 Auto。 |
| WarningLevel | 指定停止页面编译的警告级别。可能的值为 0 到 4。 |

以下是使用 `@Page` 指令的示例：

```
<@ Language="VB" AutoEventWire="false" CodeFile="Default.aspx.vb"
Inherits="_Default" %>
```

## @Master

`@Master` 指令与 `@Page` 指令非常相似，区别在于 `@Master` 指令用于主页（.master）。在使用 `@Master` 指令时，你指定了模板页面的属性，这些属性将与你网站上的任意内容页面配合使用。任何内容页面（使用 `@Page` 指令构建）都可以继承使用 `@Master` 指令的主页的所有主项。尽管它们很相似，但 `@Master` 指令可用的属性比 `@Page` 指令要少。`@Master` 指令的可用属性见表 1-5。

表 1-5
| 属性 | 说明 |
|---|---|---|
| AutoEventWire | ClassName | CodeFile | CompilationMode | CompilerOptions | CompileWith | Debug | Description | EnableTheming | EnableViewState | Explicit | Inherits | Language | LinePragmas | MasterDetailPage | Src | Strict | WarningLevel |
| 设置为 True 时，指定主页事件是否自动接线。默认设置为 True。 | 指定编译时绑定到主页的类名。 | 引用与页面关联的后台代码文件。 | 指定 ASP.NET 是否应该编译该页面。可用选项包括 Always（默认值）、Auto 或 Never。设置为 Auto 意味着如果可能，ASP.NET 将不会编译该页面。 | 编译器字符串指示主页的编译选项。 | 接收一个指向用于主页的后台代码文件的字符串值。 | 设置为 True 时，带调试符号编译主页。 | 提供主页的文本描述。ASP.NET 解析器忽略此属性及其分配的值。 | 设置为 True 时，表示主页启用启用主题（theming）。默认设置为 False。 | 设置为 True 时，维护主页的视图状态（ViewState）。默认值为 True。 | 设置为 True 时，表示启用了 Visual Basic 的 Explicit 选项。默认设置为 False。 | 指定主页继承的后台代码类（CodeBehind class）。 | 定义用于任何内联渲染和脚本块的语言。 | 布尔值指定生成的程序集是否使用行指令（line pragmas）。 | 接收一个指向与主页使用的主页位置的字符串值。主页可以使用另一个主页，从而创建嵌套主页。 | 指向用于渲染的主页后台代码的类源文件。 | 设置为 True 时，使用 Visual Basic Strict 模式编译主页。默认设置为 False。 | 指定你想要终止页面编译的警告级别。可能的值从 0 到 4。 |

以下是使用 `@Master` 指令的示例：

```
<@Master Language="VB" CodeFile="MasterPage.master.vb"
AutoEvent="false" Inherits="MasterPage %>
```

## Control

`@Control` 指令与 `@Page` 指令相似，区别在于 `@Control` 用于 ASP.NET 用户控件（user control）。`@Control` 允许在解析和编译时为用户控件定义属性。可用的属性比 `@Page` 指令少。表 1-6 定义了这些属性。

表 1-6
| 属性 | 说明 |
| --- | --- |
| AutoEventWire | ClassName | CodeFile | CompilationMode | CompilerOptions | CompileWith | Debug | Description | EnableTheming | EnableViewState | Explicit | Inherits | Language | LinePragmas | Src | Strict | WarningLevel |
| 设置为 True 时，指定用户控件事件是否自动接线。默认设置为 True。 | 指定编译时绑定到用户控件的类名。 | 引用与页面关联的后台代码文件。 | 指定 ASP.NET 是否应该编译该用户控件。可用选项包括 Always（默认值）、Auto 或 Never。设置为 Auto 意味着如果可能，ASP.NET 将不会编译该页面。 | 编译器字符串指示用户控件的编译选项。 | 接收一个指向用于用户控件的后台代码文件的字符串值。 | 设置为 True 时，带调试符号编译用户控件。 | 提供用户控件的文本描述。ASP.NET 解析器忽略此属性及其分配的值。 | 设置为 True 时，表示用户控件启用主题。默认设置为 False。 | 设置为 True 时，维护用户控件的视图状态。默认值为 True。 | 设置为 True 时，表示启用了 Visual Basic 的 Explicit 选项。默认设置为 False。 | 指定用户控件继承的后台代码类。 | 定义用于任何内联渲染和脚本块的语言。 | 布尔值指定生成的程序集是否使用行指令。 | 指向用于渲染的用户控件后台代码的类源文件。 | 设置为 True 时，使用 Visual Basic Strict 模式编译用户控件。默认设置为 False。 | 指定你想要终止页面编译的警告级别。可能的值从 0 到 4。 |

以下是使用它的示例：

```
<%Control Language="VB" Explicit='True"
CodeFile="WebUserControl.ascx.vb" Inherits="WebUserControl"
Description="This is the registration user control." %>
```

# @Import

`@Import` 指令允许你指定一个命名空间，将其导入到 ASP.NET 页面或用户控件中。通过导入该命名空间，命名空间中的所有类和接口都对页面或用户控件可用。此指令仅支持一个属性：Namespace（命名空间）。

Namespace 属性接受一个字符串值，指定要导入的命名空间。`@Import` 指令不能包含多个一个属性/值对。因此，你必须按照所示，将多个命名空间放在不同的行中，如文所示：

```xml
<@ Import Namespace="System.Data" %>
<%@ Import Namespace="System.Data.SqlClient" %>
```

你的应用程序已经引用了几个程序集。你可以通过查看位于 `C:\Windows\Microsoft.NET\Framework\v4.0.XXXXX` 下的 `web.config` 文件来查找这些程序集的列表。你可以从 `<compilation>` 设置下的 `<assemblies>` 子元素找到此程序集列表。`web.config` 文件中的设置如下：

```xml
<assemblies>
  <assembly name="mscorlib" />
  <assembly name="System.CSharp,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b775a56" />
  <assembly name="System,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Configuration,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Web,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Data,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Services,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Xml,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Hosting,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.EnterpriseServices,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
  <assembly name="System.Web.Handlers,Version=4.0.0.0, Culture=neutral, PublicKeyToken=b7a5c56193ae0899" />
```
