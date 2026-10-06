

```fsharp
let b = x - x / 10 * 10
? (a*2* b)
```

```fsharp
let data = [-100..100]
let resultData = data | List.filter (7)
```

```fsharp
// test data
let oracle =
    data
    | List.filter (fun n -> n % 7 = 0)
let c = resultData = oracle
```

注意：此示例展示了如何在函数名中使用特殊字符。除了要求活动模式（active pattern）名称必须以大写字母开头外，F# 对命名没有其他任何限制。你甚至可以在函数名中使用 Unicode 字符。
你可以使用 F# 交互式 (FSI)，通过键盘上的 Alt+数字键来输入字符并打印列表，FSI 将能够识别出这些字符。这里显示了一个示例。第一个字符是 Alt + 900，最后一个是 Alt + 980。如果你的系统没有键盘，可以使用 Microsoft Word 等其他系统来生成这些字符。

```fsharp
> ['à','...'];
val it : char list = [
['à'; 'á'; 'â'; 'ä'; 'è'; 'ë'; 'í'; 'î'; 'ï'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'];
['A'; 'Á'; 'Ã'; 'Ä'; 'E'; 'Ê'; 'Ë'; 'Í'; 'Î'; 'Ï'; 'Ò'; 'Ó'; 'Ö'; 'Õ'; 'Ú'];
['C'; 'Ç'; 'Œ'; 'É'; 'E'; 'Ê'; 'Ë'; 'Í'; 'Î'; 'Ï'; 'Ò'; 'Ó'; 'Ö'; 'Õ'; 'Ú'];
['D'; 'Ð'; 'E'; 'É'; 'ê'; 'ë'; 'í'; 'î'; 'ï'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'];
['G'; 'Ğ'; 'Ĝ'; 'H'; 'Ħ'; 'í'; 'î'; 'ï'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'];
['I'; ' ''; ''; 'í'; 'î'; 'ï'; 'ñ'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'; 'ú'; 'ý'; 'ÿ'];
['L'; 'Ł'; 'Ĺ'; 'ļ'; 'ñ'; 'ò'; 'ó'; 'ö'; 'õ'; 'ù'; 'ý'; 'ÿ'];
['N'; 'Ñ'; 'ń'; 'ò'; 'ó'; 'ö'; 'õ'; 'ý'; 'ÿ']; ...
```

# 开发 WinRT 应用

在 Visual Studio 2012 中，F# 自带了一个新模板：“可迁移库”（Portable Library）。该模板用于开发 WinRT 应用。在开发 WinRT 应用时，可以使用 F# 可迁移库来托管业务逻辑。
可迁移库是 .NET 框架 Silverlight、桌面端和 WinRT 的交集。由于可迁移库是这些 .NET 框架的子集，将应用程序从桌面环境移动到可迁移库在某些情况下不可行（例如，Silverlight 框架不支持）。
如果你想为 WinRT 应用开发业务逻辑，F# 可迁移库是一个很好的选择。F# 可迁移库被设计在 Windows Store 应用、Silverlight 应用和桌面应用程序中执行。你现在将创建一个 Windows Store 应用，它作为本章示例的 UI 控制器。
当你创建一个新项目时，可以在 Visual Studio 2012 中展开“Windows Store”节点并选择“空白应用”模板，如图 7-6 所示。

![](img/63aaf94e22830ab98ce16c946be8ef6_406_png)

F# 3.0 的版本包含了一些设置，导致 Windows 8 应用的验证失败。这个 Windows 8 验证 Bug 在 Visual Studio Update 中已修复。如果没有安装 Visual Studio Update，可以通过编辑项目的 文件来解决此问题：

```xml
<PropertyGroup Condition="$(Configuration)|$(Platform) == 'Release|AnyCPU'">
    <OtherFlags>-staticlink:FSharp.Core</OtherFlags>
</varnothing>
```

# 新项目

- 最近
- 已安装
- Visual C#
- 其他语言
- Visual Basic
- Windows Store
- Office
- SharePoint
- Unity

**排序方式：**

| Visual C# | Visual C# |
|---|---|
| 空白应用 (XAML) | 使用定义控件或布局的 Windows Store 简单项目。 |
| 分类应用 (XAML) | |
| 类库 (Windows Store 应用) | |
| 运行时组件 | |
| 单元测试库 (Windows... | |

- 在线
- 名称：WinUI
- 位置：C:\Projects\
- 解决方案名称：WinUI

**图 7-6** 创建 Windows Store 应用 (XAML) 项目

生成的解决方案示例如图 7-7 所示。

![](img/63aaf94e22830ab98ce16c946be8ef6_407.png)

**图 7-7** 从空白模板生成的 Windows 8 应用

在属性页面，F# 可迁移库可以配置为目标 WinRT、.NET 4.5 和 Silverlight 5。见图 7-8。

| 配置：可用 | 平台：可用 |
|---|---|
| 生成 | |
| 生成事件：WinUI | |
| 调试 | |
| 引用路径 | |
| 目标框架：.NET 迁移子集 (Windows Store 应用) | 输出：类库 |
| .NET 迁移子集 (Windows Store 应用, .NET 4.5, Silverlight 5) | |
| 资源： | |
| 指定如何管理应用程序资源： | |
| 资源文件： |

**图 7-8** 可迁移库项目页

第三部分 现实应用

你可以在表单中添加文本块，如列表 7-4 所示。

# 列表 7-4 表单中的 XAML 代码

```xml
<Page
  x:Class="WinUI.MainPage"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:local="http://schemas.microsoft.com/expression/blend/2008"
  xmlns:mc="http://schemas.microsoft.com/expression/xmlformats/markup-compatibility/2006"
  mc:Ignorable="d">

  <Grid Background="{StaticResource ApplicationPageThemeBrush}">
    <TextBlock x:Name="result_box" Text="Result"/>
  </Grid>
</Page>
```

现在可以在解决方案中创建 F# 可迁移库项目，如图 7-9 所示。

![](img/63aaf94e22830ab98ce16c946be8ef6_408_0.png)

**图 7-9** 在 Win8UI 解决方案中创建 F# 可迁移库

带有 F# 可迁移类库项目的新解决方案结构如图 7-10 所示。

# 解决方案资源管理器

![](img/63aaf94e22830ab98ce16c946be8ef6_409_0.png)

**图 7-10** 带有 F# 可迁移类库的解决方案结构

