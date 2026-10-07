
`App.xaml` 和 `App.cs` 文件实际上定义了 `App` 类的部分。在编译期间，Visual Studio 会解析 `App.xaml` 并生成另一个名为 `App.g.cs` 的文件。“g” 代表 "generated"（生成的）。如果你查看此文件，可以在项目的 `\obj\` 子目录中找到它。`App.g.cs` 文件包含了 `App` 类的另一个部分定义，并且它包含一个名为 `InitializeComponent` 的方法，该方法在 `App.cs` 文件的构造函数中调用。

你可以自由编辑 `App.xaml` 和 `App.cs` 文件，但不要乱动 `App.g.cs`。该文件在构建项目时会重新创建。

# 第一章 你好，Windows Phone 7

当程序运行时，`App` 类会创建一个 `PhoneApplication` 类型的对象，并将该对象设置为它自己的 `RootVisual` 属性。这个框架宽 480 像素，高 800 像素，占据了手机的整个显示区域。`PhoneApplication` 通过导航到名为 `MainPage` 的对象，其行为有点类似于网页浏览器。

`MainPage` 是每个 Silverlight 程序中的第二个类，定义在第二对文件 `MainPage.xaml` 和 `MainPage.xaml.cs` 中。在较小的 Silverlight 程序中，你花费的大部分时间都会在这两个文件上。

除了一堆 `using` 指令列表外，`MainPage.xaml.cs` 文件非常简单：

```csharp
Silverlight 项目：SilverlightHello 文件：MainPage.xaml.cs (节选)
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.SilverlightHello
namespace SilverlightHelloPhone
{
    public partial class MainPage : PhoneApplicationPage
    {
        // 构造函数
        public MainPage()
        {
            InitializeComponent();
        }
    }
}
```

以 `System.Windows` 开头的命名空间的 `using` 指令用于 Silverlight 类；有时你可能还需要其他指令来补充这些。`Microsoft.Phone.Controls` 命名空间包含了针对手机的 Silverlight 扩展，包括 `PhoneApplication` 类

再次，我们看到了另一个部分类定义。它定义了一个名为 `MainPage` 的类，该类派自 Silverlight 类 `PhoneApplicationPage`。这个类定义了当你运行 `SilverlightHelloPhone` 程序时在屏幕上实际看到的视觉效果。

## 第一部分 基础知识

`MainPage` 类的另一半定义在 `MainPage.xaml` 文件中。这是一个几乎完整的文件，为了适应分页进行了稍微重新格式，并排除了末尾被注释掉的部分，但仍然是一段相当惊人的标记：

Silverlight 项目：SilverHelloPhone 文件：MainPage.xaml（几乎完整）

```xml
<phone:PhoneApplicationPage
x:Class="SilverlightHelloPhone.MainPage"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:phone="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone"
xmlns:shell="clr-namespace:Microsoft.Phone;assembly=Microsoft.Phone"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.microsoft.com/openxml.org/markup-compatibility/2006"
mc:ignorable="d" d:DesignWidth="480" d:DesignHeight="768"
FontFamily={StaticResource PhoneFontNormal}"
FontSize={StaticResource PhoneFontSizeNormal}"
Foreground={StaticResource PhoneForegroundBrush}"
SupportedOrientations="Portrait" Orientation="Portrait"
shell:SystemTray.IsVisible="True">

  <!-- LayoutRoot 是所有内容的网格 -->
  <Grid Name="LayoutRoot" Background="Transparent">
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="*"/>
  </Grid>

  <!-- TitlePanel 包含应用程序名称和标题 -->
  <StackPanel Name="TitlePanel" Grid.Row="0" Margin="12,17,0">
    <TextBlock Name="Application" Text="MY"
               Style={StaticResource TitleStyle}"/>
    <TextBlock Name="PageTitle" Text="page" Margin="9,-7,0"
               Style={StaticResource TitleStyle}"/>
  </StackPanel>

  <!-- ContentPanel - 在此处放置额外内容 -->
  <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12">
  </Grid>
</LayoutRoot>
</phone:PhoneApplicationPage>
```

前四个命名空间声明与 `App.xaml` 相同。在 `App.xaml` 文件中，`x:Class` 属于根元素。这指示 `MainPage` 类派自 Silverlight `PhoneApplication` 类。

`d`（设计器）和 `mc`（用于标记兼容性）命名空间声明是为了设计程序的便利。`DesignerWidth` 和 `DesignerHeight` 属性在编译期间会被忽略。

程序的编译会生成另一个包含部分定义的 `MainPage.cs` 文件。然而，有时当程序抛出异常时，这些文件中的一个出现在你面前。这有助于你在它们出现之前理解问题。但是，不要尝试通过编辑这些文件来修复问题！问题可能位于 XAML 文件的某处。

在 `MainPage.xaml` 的根元素中，你会看到影响页面的 `FontFamily`、`FontSize` 和 `Foreground` 设置。我在第 7 章介绍 `StaticResource` 和这种语法。

`MainPage.xaml` 的主体包含了几个嵌套的元素，如 `Grid`、`StackPanel` 和 `TextBlock`。

注意“元素”这个词：在 Silverlight 编程中，这个词有两个相关的含义。它是一个 XML 术语，用于指示由起始标记和结束标记界定的项目。它也是 Silverlight 中用于指视觉对象的词，事实上，这个词出现在两个实际 Silverlight 类的名称中。

你在 Silverlight 中使用的许多类都是这个重要的类层次结构的一部分

+   Object

  DependencyObject（抽象）

    UIElement（抽象）

      FrameworkElement（抽象）

除了 *UIElement* 之外，其他 Silverlight 类派生自 *DependencyObject*。但 *UIElement* 的区别在于它是能够作为视觉对象出现在屏幕上并接收用户输入的类。（在 Silverlight 中，所有视觉对象都可以接收用户输入。）

派自 *UIElement* 的唯一类是 *FrameworkElement*。这两个类之间的区别是 Windows Presentation Foundation 的历史产物。在 WPF 中，开发者可以通过派生 `UIElement` 来创建他们独特的框架。在 Silverlight 中这是不可能的，因此这种区别毫无意义。

派自 *FrameworkElement* 的类之一是 `Control`，在传统的图形用户界面编程中这个词比“元素”更常见。某些对象

## 第一部分 基础

在其他编程环境中被称为控件（controls），在 Silverlight 中更准确的称应该是元素（elements）。控件派生类包括按钮和滑动条，我将在第 10 章中讨论它们。

另一个派自 FrameworkElement 的类是 Panel，它是你在 MainPage.xml 中看到的 Grid 和 StackPanel 元素的父类。Panel 元素可以包含多个子元素并在屏幕上以各种方式排列它们。我将在第 9 章中深入讨论面板。

另一个派自 FrameworkElement 的类是 TextBlock，这是你在显示长度最多一个段落的文本块时最常用的元素。MainPage.xml 中的两个 Text 元素显示了新 Silverlight 程序中的两个标题部分。

PhoneApplication、Grid、StackPanel 和 TextBlock 都是 Silverlight 类。在标记（Markup）中，它们变为 XML 元素。这些类的属性变为 XML 属性。

MainPage.xml 中元素的嵌套被称为定义了一个视觉树（visual tree）。在适用于 Windows Phone 7 的 Silverlight 程序中，视觉树始终从 PhoneApplicationFrame 类型的对象开始，它占据了手机的整个视觉表面。

Windows Phone 7 的 Silverlight 程序始终有一个且仅有一个 PhoneApplicationFrame 实例，非正式称为帧（frame）。

相比之下，程序可以有多个 PhoneApplicationPage 实例，非正式称为页面（page）。在任何时候，帧都持有一个页面，但允许你导航到其他页面。默认情况下，页面不占据帧的整个显示表面，因为它为手机顶部的系统栏（也称为状态栏）留出了空间。

我们简单的应用程序只有一个页面，恰恰地称为 MainPage。这个 MainPage 包含一个 Grid，Grid 包含一个带有几个 TextBlock 元素的 StackPanel 以及另一个 Grid，它们都在一个分级树中。Silverlight 程序的视觉树在 Visual Studio 中创建：

```
PhoneApplicationFrame
  PhoneApplicationPage
    Grid named "LayoutRoot"
      StackPanel named "TitlePanel"
        TextBlock named "ApplicationTitle"
        TextBlock named "PageTitle"
    Grid named "ContentPanel"
```

我们最初的目标是创建一个在显示器中心显示某些文本的 Silverlight 程序，但考虑到有几个标题，让我们将其修改为在标题之外的页面中心显示该文本。程序内容的区域是文件底部的 Grid，前面带有注释“ContentPanel - place additional here.”。该 Grid 的名称为“ContentPanel”，我将非正式地称之为“内容面板”或“内容网格”。除了标题之外，对应此 Grid 的屏幕区域我通常称为“内容区域”。

在网格中，你可以插入一个新的 TextBlock：

Silverlight 项目: SilverlightHelloPhone 文件: MainPage.xaml (节选)

```xml
<Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
    <TextBlock Text="Hello, Windows Phone 7"
               HorizontalAlignment="Center"
               VerticalAlignment="Center" />
</Grid>
```

Text、HorizontalAlignment 和 VerticalAlignment 都是 TextBlock 类的属性。Text 属性的类型是 string。HorizontalAlignment 和 VerticalAlignment 属性分别是多种 HorizontalAlignment 和 VerticalAlignment 类型。当你需要在 XAML 中引用枚举类型（enumeration type）时，你只需要成员名。

当你编辑 MainPage.xaml 时，可能还想修复其他 TextBlock 元素，使其不再是通用的。将

```xml
<TextBlock ... Text="MY APPLICATION" ... />
```

改为

```xml
<TextBlock ... Text="SILVERLIGHT HELLO PHONE" ... />
```

并将

```xml
<TextBlock ... Text="page title" ... />
```

改为：

```xml
<TextBlock ... Text="main page" ... />
```

在只有一个只有一个页面的 Silverlight 应用程序中设置页面标题没有太大意义，如果你愿意，可以删除第二个 TextBlock。对此 XAML 文件的更改将反映在设计视图中。你现在可以编译并运行此程序了：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_32_0.png)

这张截图——以及书中剩余的一些截图——以接近实际手机大小的显示在书的页面上，周围环绕着一些简单的“外壳（chrome）”，它们象征着真实的手机或手机模拟器。

尽管程序很简单，但它演示了 Silverlight 编程的一些基本概念，包括动态布局。XAML 文件定义了视觉树中元素的布局。这些元素能够动态地排列自己。HorizontalAlignment 和 VerticalAlignment 属性可以将一个元素放置在另一个元素的中心，或者（正如你可能想的那样）沿着其中一个边缘或其中一个角。TextBlock 是你可以在 Silverlight 程序中使用的许多可能元素之一；其他还包括位图图像、电影以及熟悉的按钮、滑动条和列表框等控件。

### 颜色主题

从手机或手机模拟器开始，点击或触摸右上角的箭头导航到设置页面，然后选择它们。Windows Phone 7 主题由背景（Background）和强调色（Accent color）组成。对于背景，你可以选择 Dark（深色背景上的浅色文本，你一直看到的）或 Light（相反）。选择 Light 主题，再次运行 SilverlightHelloPhone，并对主题颜色自动应用感到满意：

![](img/d9347c1f55fa6d523479d2cd9b4d5459_33_0.png)

尽管程序很简单，但它演示了 Silverlight 编程的一些基本概念，包括动态布局。XAML 文件定义了视觉树中元素的布局。这些元素能够动态地排列自己。HorizontalAlignment 和 VerticalAlignment 属性可以将一个元素放置在另一个元素的中心，或者（正如你可能想的那样）沿着其中一个边缘或其中一个角。TextBlock 是你可以在 Silverlight 程序中使用的许多可能元素之一；其他还包括位图图像、电影以及熟悉的按钮、滑动条和列表框等控件。

在网格中，你可以插入一个新的 TextBlock：

Silverlight 项目: SilverlightHelloPhone 文件: MainPage.xaml (节选)

```xml
<Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
    <TextBlock Text="Hello, Windows Phone 7"
               HorizontalAlignment="Center"
               VerticalAlignment="Center" />
</Grid>
```
