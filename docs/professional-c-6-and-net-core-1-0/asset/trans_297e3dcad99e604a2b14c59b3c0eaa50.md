

Dictionary1.xaml 定义了两个资源：键为 CyanGradientBrush 的 LinearGradientBrush，以及一个可通过 PinkButtonStyle 键引用的 Button 样式（代码文件下载 ResourcesLib[WPF|UWP]/Dictionary1.xaml）：

```
<ResourceDictionary
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <LinearGradientBrush x:Key="CyanGradientBrush" StartPoint="0,0" EndPoint="0.3,1">
        <LinearGradientBrush.GradientStops>
            <GradientStop Offset="0.0" Color="LightCyan" />
            <GradientStop Offset="0.14" Color="Cyan" />
            <GradientStop Offset="0.7" Color="DarkCyan" />
        </LinearGradientBrush.GradientStops>
    </LinearGradientBrush>

    <Style x:Key="PinkButtonStyle" TargetType="Button">
        <Setter Property="FontSize" Value="22" />
        <Setter Property="Foreground" Value="White" />
        <Setter Property="Background">
            <Setter.Value>
                <LinearGradientBrush StartPoint="0,0" EndPoint="0,1">
                    <LinearGradientBrush.GradientStops>
                        <GradientStop Offset="0.0" Color="Pink" />
                        <GradientStop Offset="0.3" Color="DeepPink" />
                        <GradientStop Offset="0.9" Color="DarkOrchid" />
                    </LinearGradientBrush.GradientStops>
                </LinearGradientBrush>
            </Setter.Value>
        </Setter>
    </Style>
</ResourceDictionary>
```

在目标项目中，需要引用该库，并将资源字典添加到字典中。可以使用多个资源字典文件，可通过 ResourceDictionary 的 MergedDictionaries 属性添加。你可以向合并的字典中添加资源字典列表。

库引用的处理方式在 WPF 和 UWP 应用之间有所不同。对于 WPF，使用 pack URI 语法。pack URI 可以指定为绝对路径，即 URI 以 pack:// 开头，或指定为相对路径，如本示例中使用。对于相对语法，包含字典的引用程序集 ResourceLibWPF 在 / 后面紧跟 ;component。Component 表示字典作为资源包含在程序集中。之后添加字典文件名 Dictionary1.xaml。如果字典添加到子文件夹中，还必须声明文件夹名称（代码文件 StylesAndResourcesWPF/App.xaml）：

```
<Application x:Class="StylesAndResourcesWPF.App"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
```

背景和深色前景，对于深色主题则为深色背景和浅色前景。两个字典中样式的键相同：SampleButtonStyle（代码文件 StylesAndResourcesUWP/Styles/SampleThemes.xaml）：

```
<ResourceDictionary
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="using:StylesAndResourcesUWP">
<ResourceDictionary.ThemeDictionaries>
<ResourceDictionary x:Key="Light">
<Style TargetType="Button" x:Key="SampleButtonStyle">
<Setter Property="Background" Value="LightGray" />
<Setter Property="Foreground" Value="Black" />
</Style>
</ResourceDictionary>
<ResourceDictionary x:Key="Dark">
<Style TargetType="Button" x:Key="SampleButtonStyle">
<Setter Property="Background" Value="Black" />
<Setter Property="Foreground" Value="White" />
</Style>
</ResourceDictionary>
</ResourceDictionary.ThemeDictionaries>
</ResourceDictionary>
```

你可以使用 ThemeResource 标记扩展来分配样式。除了使用不同的标记扩展外，其他一切与使用 StaticResource 标记扩展相同（代码文件 StylesAndResourcesUWP/ThemeDemoPage.xaml）：

```
<Button Style="{ThemeResource SampleButtonStyle}" Click="OnChangeTheme" Content="Change Theme" />
```

根据所选主题，将使用相应的样式。

## 选择主题

选择主题有不同方式。首先，应用本身有一个默认值。Application 类的 RequestedTheme 属性定义了应用的默认主题。这是在 App.xaml 中定义的，也是主题字典文件被引用的位置（代码文件 StylesAndResourcesUWP/App.xaml）：

```
<Application
x:Class="StylesAndResourcesUWP.App"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:local="using:StylesAndResourcesUWP"
RequestedTheme="Light">
<Application.Resources>
<ResourceDictionary>
<ResourceDictionary.MergedDictionaries>
<ResourceDictionary Source="ms-appx:///StylesLib/Dictionary1.xaml" />
```

```
<ResourceDictionary Source="Styles/SampleThemes.xaml" />
</ResourceDictionary.MergedDictionaries>
</ResourceDictionary>
</Application.Resources>
</Application>
```

RequestedTheme 属性在 XAML 元素层次结构中定义。每个元素都可以为自身及其子元素覆盖要使用的主题。以下 Grid 元素将默认主题更改为 Dark 主题。现在这是 Grid 及其所有子元素使用的主题（代码文件 StylesAndResourcesUWP/ThemeDemoPage.xaml）：

```
<Grid x:Name="grid1"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}"
    RequestedTheme="Dark">
    <Button Style="{ThemeResource SampleButtonStyle}"
Click="OnChangeTheme"
        Content="Change Theme" />
</Grid>
```

你也可以通过代码动态更改主题，方法是设置 RequestedTheme 属性（代码文件 StylesAndResourcesUWP/ThemeDemoPage.xaml.cs）：

```
private void OnChangeTheme(object sender, RoutedEventArgs e)
{
    grid1.RequestedTheme = grid1.RequestedTheme ==
ElementTheme.Dark ?
        ElementTheme.Light: ElementTheme.Dark;
}
```

> 注意 仅当资源应根据主题显示不同时，使用 ThemeResource 标记扩展才有用。如果资源在所有主题下应保持相同，请继续使用 StaticResource 标记扩展。

## 模板

XAML Button 控件可以包含任何内容。内容可以是简单文本，但你也可以添加 Canvas 元素，其中可包含形状；Grid；或视频。事实上，你可以用按钮做更多！对于基于模板的 XAML 控件，控件的功能与其外观完全分离。按钮有一个默认外观，但你可以完全自定义该外观。

WPF 和 UWP 应用提供了几种派生自基类 FrameworkTemplate 的模板类型。

| 模板类型 | 描述 |
|---|---|
| ControlTemplate | 使你能够指定控件的视觉结构并覆盖其外观。 |
| ItemsPanelTemplate | 对于 ItemsControl，你可以通过分配 ItemsPanelTemplate 来指定其项目的布局。每个 ItemsControl 都有默认的 ItemsPanelTemplate。对于 MenuItem，它是 WrapPanel。StatusBar 使用 DockPanel，ListBox 使用 VirtualizingStackPanel。 |
| DataTemplate | 这些对于对象的图形表示非常有用。在设置 ListBox 样式时，默认情况下 ListBox 的项目是根据 ToString 方法的输出显示的。通过应用 DataTemplate，你可以覆盖此行为并定义项目的自定义呈现。 |
| HierarchicalDataTemplate | 用于排列对象树。此控件支持 HeaderedItemsControls，例如 TreeViewItem 和 MenuItem。此模板类仅在 WPF 中可用。 |

> **注意** *HierarchicalDataTemplate 在第 34 章“使用 WPF 的 Windows 桌面应用程序”中与 TreeControl 一并讨论。*

## 控件模板

在本章前面你已看到如何设置控件属性的样式。如果设置控件的简单属性无法获得所需的外观，你可以更改 Template 属性。通过 Template 属性，你可以自定义控件的完整外观。下一个示例演示如何自定义按钮，后续章节中列表视图将逐步自定义，以便你可以看到更改的中间结果。

你在一个单独的资源字典文件中自定义 Button 类型：ControlTemplates.xaml。在这里，定义了一个键名为 RoundedGelButton 的样式。样式 RoundedGelButton 设置了 Background、Height、Foreground 和 Margin 属性，以及 Template。Template 是此样式中最有趣的部分。Template 指定了一个仅有一行一列的 Grid。

在此单元格内，你可以找到一个名为 GelBackground 的椭圆。此椭圆的描边使用线性渐变画刷。围绕矩形的描边非常细，因为 StrokeThickness 已设置
