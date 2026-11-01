
## 第二部分

## Windows 编程

- ► 第 14 章：基础桌面编程
- ► 第 15 章：高级桌面编程

- 可用于各种情况的动画分镜，包括用户触发的事件，例如按钮上的鼠标点击
- 可用于动态设置控件样式的可重用资源

## 关注点分离

多年来维护 Windows 应用程序存在的一个问题是，它们经常混合生成用户界面的代码和基于用户操作执行的代码。这使得多个开发人员和设计师难以在同一项目上协作。WPF 以两种方式解决了这个问题。首先，通过使用 XAML 而不是 C# 来描述 GUI，GUI 变得平台无关，实际上你甚至可以在没有任何代码的情况下渲染 XAML。其次，这意味着将 C# 代码放在与 GUI 代码不同的文件中感觉很自然。Visual Studio 使用一种称为代码后置文件的机制，这些是与 XAML 文件动态链接的 C# 文件。

由于 GUI 与代码分离，可以创建用于设计 GUI 的定制应用程序，而微软正是这样做的。Blend for Visual Studio 设计工具是设计师在为 WPF 创建 GUI 时最青睐的工具。该工具可以加载与 Visual Studio 相同的项目，但 Visual Studio 更侧重于开发人员，而 Expression Blend 则相反。这意味着在拥有设计师和开发人员的庞大项目中，每个人都可以使用自己偏好的工具在同一项目上协作，而不必担心无意中影响他人。

## XAML 实践

如前所述，XAML 是 XML，这意味着只要文件不太大，就能立即看出它描述了什么。看看这个小例子，看看你能否判断它做了什么：

```
<Window x:Class="Ch14Ex01.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:local="clr-namespace:WpfApplication1"
    mc:Ignorable="d"
    Title="Hello World" Height="350" Width="525">
    <Grid>
        <Button Content="Hello World"
            HorizontalAlignment="Left"
            Margin="220,151,0,0"
            VerticalAlignment="Top"
            Width="75"/>
    </Grid>
</Window>
```

此示例中的 XAML 创建了一个带有单个按钮的窗口。窗口和按钮都显示文本“Hello World”。XML 允许你在正确闭合标签的前提下将标签嵌套在其他标签内。当 XAML 中一个元素被放置在另一个元素内部时，该元素成为包含元素的 content，这意味着 Button 也可以这样写：

```
<Button HorizontalAlignment="Left"
Margin="220,151,0,0"
VerticalAlignment="Top"
Width="75"
    Hello World
</Button>
```

这里，Button 的 Content 属性已被移除，文本现在是 Button 控件的子节点。在 XAML 中，Content 可以是几乎任何东西，这在示例中也有体现：Button 元素是 Grid 元素的内容，而 Grid 元素本身是 Window 元素的内容。

大多数，如果不是全部，控件都可以有内容，并且改变内置控件外观的限制非常少。第 15 章更详细地探讨了这一点。

## 命名空间

前例中的 Window 元素是 XAML 文件的根元素。该元素通常包含多个命名空间声明。默认情况下，Visual Studio 设计器包含两个你应该注意的命名空间：http://schemas.microsoft.com/winfx/2006/xaml/presentation 和 http://schemas.microsoft.com/winfx/2006/xaml。第一个是 WPF 的默认命名空间，声明了大量用于创建用户界面的控件。第二个声明 XAML 语言本身。命名空间不必在根标签上声明，但这样做可以确保其内容在整个 XAML 文件中易于访问，因此几乎不需要移动声明。

> 注意 命名空间看起来像是 URL，但这具有误导性。事实上它们被称为统一资源标识符（URI）。只要 URI 能唯一标识一个资源，它可以是任何字符串。微软选择以通常用于 URL 的形式指定这些 URL，但如果你在浏览器中输入它们，将不会得到任何结果。

当你在 Visual Studio 中创建新窗口时，呈现命名空间始终声明为默认命名空间，语言命名空间声明为 xmlns:x。如 Window、Button 和 Grid 标签所示，这确保你不必为添加到窗口的控件添加前缀，但指定的语言元素必须以 x 为前缀。

你经常会看到的最后一个命名空间是系统命名空间：xmlns:sys="clr-namespace:System;assembly=mscorlib"。该命名空间允许你在 XAML 中使用 .NET Framework 的内置类型。通过这样做，你编写的标记可以显式声明正在创建的元素类型。例如，可以在标记中声明一个数组并说明数组的成员是字符串：

```
<Window.Resources>
<ResourceDictionary>
```

顺便说一下，也展开面板中的“常用 WPF 控件”节点。你将在本章中使用这里显示的大多数控件。

## WPF 控件

控件结合了预打包的代码和可用于创建更复杂应用程序的 GUI。它们可以定义默认的绘制方式和一组标准行为。一些控件，例如 `Label`、`Button` 和 `TextBox` 控件，易于识别，并且在 Windows 应用程序中已使用了约 20 年。其他控件，例如 `Canvas` 和 `StackPanel`，不显示任何内容，只是帮助你创建 GUI。

开箱即用的控件看起来就像你在标准 Windows 应用程序中期望控件的样子，并使用当前的 Windows 主题来绘制自己。所有这些都高度可定制，只需几次点击即可完全改变控件的显示方式。这种定制是通过控件上定义的属性完成的。WPF 使用你之前见过的普通属性，并增加了一种名为 `dependency property` 的新属性类型。这些将在第 15 章中详细讨论，但现在知道 WPF 的许多属性不仅仅是获取和设置值就足够了；例如，它们能够通知观察者更改。

除了定义屏幕上事物的外观外，控件还定义标准行为，例如点击按钮和在列表中选择某项的能力。你可以通过“处理”控件定义事件来改变用户对控件执行操作时发生的事情。事件处理程序的实现方式和时间因应用程序和控件而异，但一般来说，你总是会处理按钮的 `Click` 事件；对于 `ListBox` 控件，当用户更改选择时你通常需要做出反应，因此应处理 `SelectionChanged` 事件。对于其他控件，例如 `Label` 或 `TextBlock` 控件，你很少会实现任何事件。

> **警告** 尽管用户通常很高兴你花时间提供比标准 Windows 显示更有趣的用户界面，但在更改控件的标准行为时必须小心。想象一下，你将 `Button` 控件更改为仅在用户右键单击时才工作。你的用户会在左键单击按钮时没有任何反应时认为你的应用程序坏了。事实上，即使有极好的理由这样更改按钮，你可能应该使用另一种类型的控件而不是更改 `Button` 控件的行为。

你可以通过多种方式向窗口添加控件，但最常见的方式是从工具箱将它们拖放到设计视图或 XAML 视图中。
