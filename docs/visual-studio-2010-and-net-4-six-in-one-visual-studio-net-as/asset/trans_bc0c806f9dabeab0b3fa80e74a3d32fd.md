
表 5-3 汇总了解决方案中最重要的文件的作用。

## 表 5-3: 启动页解决方案结构文件

| 文件 | 说明 |
|---|---|
| ReadMe.txt | 该文件包含关于运行和部署解决方案的简要说明和描述。 |
| source.extension.vsixmanifest | 此文件定义了在安装扩展期间使用的部署清单信息。 |
| StartPage.bmp | 此文件包含在扩展管理器（Extension Manager）和 Visual Studio Gallery 中表示扩展的图标。 |
| StartPage.pkgdef | 此文件描述了部署期间要合并到注册表的信息。 |
| StartPage.xaml | 此 XAML 文件定义了启动页的视觉外观。它是默认启动页的克隆，添加了一个可以自定义的新的 MyControl 标签页。 |
| StartStartPreview.png | 此文件包含在扩展管理器和 Visual Studio Gallery 中表示扩展的预览图像。 |
| MyControl.xaml MyControl.cs | 这些文件可以在 SimpleStartControl 项目中找到。它们定义了代表 MyControl 标签的 WPF 用户控件。 |

除了这些文件，解决方案的两个项目还引用了一些程序集。表 5-4 汇总了它们的作用和说明。

## 表 5-4: 启动页解决方案结构程序集

| 程序集 | 说明 |
|---|---|
| Microsoft.VisualStudio.Shell.10.0 | 该程序集随 Visual Studio 2010 SDK 发布。它包含与新的 Visual Studio 2010 shell 相关的类型和资源。两个项目引用此程序集，并使用它访问 shell 相关资源（例如用于绘制 IDE UI 的预定义笔和画刷）。 |
| Microsoft.VisualStudio.Shell.StartPage | 该程序集随 Visual Studio 2010 SDK 发布。在这里定义的类型和资源用于启动页。例如，此程序集包含了 `MruListBox` 的定义，用于显示最近的项目，或启动页使用的图像资源。 |
| UIAutomationProvider, UIAutomationTypes | 这两个程序集用于创建 UI 自动化程序，以便 UI 控件不仅可以通过人工交互，还可以通过自动化对象访问。在自定义启动页模板生成的默认源代码中没有使用这些程序集。 |

## 启动页的定义

SimpleStartPage 项目中的 StartPage.xml 定义了启动页的本质。你可以看到 StartPage.xml 没有代码文件，其 Build Action（生成操作）属性是 Content（内容）。原因是 Visual Studio 会在启动时动态加载并解析 XML 文件，而不是从 SimpleStartPage 程序集加载二进制表示。

当然，这并不意味着你不能为 StartPage.xml 分配代码，但你必须这样做，以便页面使用在外部程序集中实现的用户定义控件。你打算使用的代码应该放在这些外部程序集中。该模板遵循这种模式；你可以向位于 SimpleStartPageControl 程序集中的 MyControl WPF 用户控件类中添加代码。

在解决方案资源管理器中双击 StartPage.xml 以打开它。如果你尚未编译解决方案，XML 编辑器可能会警告你无法在 WPF 设计器中显示该页面。在生成解决方案后，你可以重新加载页面。

你可以观察到的第一点是页面的样式与你在活动启动页中看到的不同。这种现象的原因是 XAML 文件中的样式引用了 Visual Studio 定义。启动页必须在运行的 Visual Studio 实例上下文中加载，以便访问这些类。

XAML 定义的结构非常简单，如列表 5-2 提取的内容所示。

> 列表 5: StartPage.xml（提取内容）

```xml
<xml xmlns="http://schemas.microsoft.com/winfx/2006/xml/presentation"
     xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
     xmlns:sp="assembly=Microsoft.VisualStudio.Shell.StartPage"
     xmlns:vs="assembly=Microsoft.VisualStudio.Shell.PlatformUI"
     xmlns:vsfx="assembly=Microsoft.VisualStudio.Shell.10.0"
     xmlns:assembly="assembly=Microsoft.VisualStudio.Shell.10.0"
     xmlns:my="assembly=SimpleStartControl"
     mc:ignorable="d"
     xmlns:d="http://schemas.microsoft.com/expression/2006/blend"
     xmlns:mc="http://schemas.openxmlformats.org/markup/2006/xaml"
     d:DesignWidth="600"
     d:DesignHeight="800">
  <Grid.Resources>
    <MergedDictionaries>
      <ResourceDictionary Source="Microsoft.VisualStudio.Shell.StartPage;Styles.xaml" />
    </MergedDictionaries>
  </Grid.Resources>
  <Grid x:Name="LayoutRoot"
    Background="DynamicResource {Brushes.BackgroundColor}"
    Style="DynamicResource StartPage.Style">
    <!-- Grid omitted -->
  </Grid>
```

*代码文件 [StartPage.xml] 可从 Wrox.com 下载* 列表中引人注目的是它的根元素是 Grid 而不是 Window 或 UserControl。这个 Grid 是包含资源并定义启动页布局的容器。从 Grid 的属性可以看出，它定义了表 5-4 中引用的程序集，以及 SimpleStartControl 程序集的标签。<Grid.Resources> 元素为页面提供了资源。带有 LayoutRoot 的 Grid 定义了启动页的内容。Visual Studio 将此 UI 嵌套到启动页。你可以看到 Microsoft.VisualStudio.Shell.10.0 程序集的 BackgroundColor 属性用于设置网格的背景![](img/b597c74e848b270d30513ae16.png)。LayoutRoot 网格包含了超过 200 行定义页面 UI 的代码。查看此 XAML 代码的一些细节将帮助你理解启动页是如何构造的。

## 命令按钮定义

Visual Studio 2010 终极版（Ultimate Edition）的启动页在 Logo 下包含三个命令按钮，如图 29 所示。这些按钮是通过列表 5-3 中的 XAML 代码定义的。

![](img/b597c74e848b270d30513ae16.png)
图 29: 启动页上的命令按钮

### 列表 5-3: StartPage.xaml（命令按钮定义）

```xml
<Grid x:Name="commandButtonsGrid" MinWidth="270" Grid.Row="0" Margin="0,15,0,30" HorizontalAlignment="Left">
  <Grid.RowDefinitions>
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="3"/>
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="3"/>
    <RowDefinition Height="Auto"/>
  </Grid.RowDefinitions>
  <ImageButton x:Id="ConnectTSSButton" Margin="15,2,15,2" Width="Auto"
    Content="Connect To Team Server"
    Visibility="{Binding Path=TeamFoundationSupported, Converter={StaticResource BoolToVisibilityConverter}}"
    Style="DynamicResource StartPage.CommandButtonStyle"
    Command="{Static sp:VSCommands.ExecuteCommand}"
    CommandParameter="..."/ConnectFoundationServer"
    ImageNormal="..."/ConnectTFSS.png"
    ImageHover="..."/ConnectTFSMouseOver.png"
    ImagePressed="..."/ConnectTFSMouseDown.png" />
  </ImageButton>
  <ImageButton Grid.Row="2" x:Id="NewProjectButton" Margin="15,2,0,2" Width="Auto"
    Content="New Project..."
    Style="DynamicResource StartPage.CommandButtonStyle"
    Command="{Static sp:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject"
    ImageNormal="..."/NewProject.png"
    ImageHover="..."/NewProjectMouseOver.png"
    ImagePressed="..."/NewProjectMouseDown.png" />
  </ImageButton>
  <ImageButton Grid.Row="4" x:Uid="OpenProjectButton"
    Margin="15,2,0,2" Width="Auto"
    Content="Open Project..."
    Style="(DynamicResource StartPage.CommandButtonStyle)"
    Command="(StaticResource VSCommand.ExecuteCommand)"
    CommandParameter="File.OpenProject"
    ImageNormal="..."/OpenProject.png"
    ImageHover="..."/OpenProjectMouseOver.png"
    ImagePressed="..."/OpenProjectMouseDown.png" />
  </ImageButton>
</Grid>
```

*代码文件 [StartPage.xml] 可从 Wrox.com 下载*

每个命令都由一个 vs:Image 类型定义（该类型在 Microsoft.VisualStudio.Shell.11.0 程序集中实现），并有几个影响其外观和行为的属性。ImageNormal、ImageHover 和 ImagePressed 属性允许为命令按钮特定特定定义图像资源。在 5-3 中，仅指示了部分内容。原始的 StartPage.xaml 文件中具有完整的资源。

x:Uid 定义了命令的唯一标识符，可用于编程方式访问它们。理论上，Command 的定义是为了执行与 CommandParameter 中的名称相标识的 Visual Studio IDE Shell。这里使用的名称与你在命令窗口（视图 > 其他窗口）中使用的名称完全相同。
