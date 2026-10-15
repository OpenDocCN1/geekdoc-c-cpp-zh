

measure-arrange 过程的最终结果取决于执行该过程的布局容器类型不同而不同。

例如，Grid 控件中包含的元素是根据列和行定义所定义的行列布局以及 UI 元素分配到特定行和列的方式进行布局的。StackPanel 中包含的元素是按顺序布局的，可以是水平或垂直方向。Border 中包含的单个元素（它本身也可以是一个布局面板） simply 出现在边框包围之下。

无论父面板使用何种布局机制，measure-arrange 过程的调用方式都是一样的。

回顾一下，Measure 阶段是确定每个元素的期望大小的地方，而 Arrange 阶段是确定每个子元素大小和位置的最终阶段。

请看下面的 XAML（如果现在还不太明白也没关系；随着你阅读本书的进展就会明白了）。请特别注意子元素出现的顺序以及每个元素如何在父面板中嵌套。图 5.1 显示了这些元素是如何被测量然后排列以产生丰富的显示效果。

```
<Grid x:Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
<Border BorderBrush="AliceBlue" BorderThickness="2">
    <StackPanel>
        <TextBlock Text="Hello"/>
        <TextBlock Text="World"/>
        <StackPanel Orientation="Horizontal">
            <TextBlock Foreground="Yellow" Text="Hello "/>
            <TextBlock Foreground="Yellow" Text=" World"/>
        </StackPanel>
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="150"/>
                <ColumnDefinition Width="200"/>
            </Grid.ColumnDefinitions>
            <Grid.RowDefinitions>
                <RowDefinition Height="150"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
            <Button Grid.Row="0" Grid.Column="0">
                <TextBlock Text="Button"/>
            </Button>
            <Button Grid.Row="0" Grid.Column="1">
                <StackPanel>
                    <TextBlock Text="Other Button"/>
                    <TextBlock Text="hi"/>
                </StackPanel>
            </Button>
        </Grid>
    </StackPanel>
</Border>
</Grid>
```

```
<TextBlock Text="Goodbye World"/>
</StackPanel>
</Border>
</Grid>
```

![](img/04a00d46bb1059867d95707babd62ee7_69_0.png)

图 5.1 嵌套的布局面板。

在前面的示例中，最外层的元素是一个 Grid。在该 Grid 内部，我们有一个 Border。在该 Border 内部是一个 StackPanel，包含多个子控件，包括其他 StackPanel、另一个 Grid 和一个 TextBlock。图 5.1 显示了所有这些嵌套布局面板是如何被测量和排列以产生输出的。还值得注意的是，你可以将一个 Button 的内容设置为一个 StackPanel，而 StackPanel 可以包含多个子元素。随着你在本书中的进展，你会看到更多使用 Silverlight 和 XAML 以及控件可以做到的技巧和令人惊叹的事情，但就本章而言，这里需要注意的重要一点是 measure-and-arrange 过程是如何在布局面板上使用以以统一、可预测的方式产生输出。

## 摘要

在本章中，我对 Silverlight 中使用的布局和渲染系统进行了简要介绍。刻意简短，本章提供的信息足以让你准备好开始构建功能齐全的 Silverlight 用户界面。了解 Silverlight 布局面板的递归、层次结构特性，将在很大程度上帮助你将来构建出色的用户界面，并在阅读本书时有所帮助。

## 从 Xcode 到 Visual Studio

> *工具通常比机器更简单；它通常用手使用，而机器经常由动物或蒸汽动力驱动。*
> 
> Charles Babbage

本章全部都是关于工具的。无论我们是否愿意承认，开发人员都无法在没有 Xcode、Visual Studio、Eclipse 或其他众多 IDE 等现代工具的帮助下生产应用程序。

本章涵盖了用于开发 iOS 应用程序的 IDE Xcode，以及用于构建 Windows Phone 7 应用程序的 IDE Visual Studio。

开发人员需要了解有关 Visual Studio 的一些基本知识，以便他们能够在该环境中顺畅高效地移动并编写应用程序，而不会让工具阻碍他们。除了 Visual Studio 2010 的概览外，我还提供了 Xcode 及其基础知识的高层次概述。

### Xcode 和 iOS 应用程序开发

Xcode 是开发人员用于构建 Mac 桌面应用程序以及 iOS 应用程序的 IDE。它是一个极其可配置的工具，允许你更改从窗口布局、是否在单个窗口中进行所有编辑、颜色以及数百种其他首选项等一切内容。

Xcode 项目的主要输出可以在 Targets 文件夹下找到。当你使用 Xcode 构建应用程序时，该应用程序就是一个目标。每个目标都由一堆源代码文件、静态链接库和作为项目一部分引用的 Frameworks 组成。例如，如果你要构建一个使用 Core Data 在手机上持久化数据的 iOS 应用程序，你必须将 `CoreData.framework` 添加到 Xcode 项目的 Frameworks 配置中。

## 第 6 章 从 Xcode 到 Visual Studio

为了进一步增加新开发人员的强大功能、功能和潜在困惑，一个 Xcode 项目可以有多个目标。事实上，开发人员会为单元测试创建目标（我将在后面的章节中再次提到单元测试），一个非常常见的场景是使用单个 Xcode 项目为 iPhone 和 iPad 生产不同的目标。这是因为 iPad 的 UI 与 iPhone 的 UI 截然不同（并且包含 iPhone 上不存在的控件）。开发人员会构建不同的 UI，但在同一个 Xcode 项目中共享相同的控制器和后端代码。

Xcode UI 就像任何其他 IDE，如 Eclipse、MonoDevelop 或 Visual Studio。图 6.1 所示的布局（我个人偏好）中，视图左侧是一个导航窗格。该窗格显示了主节点，即项目根节点。双击它（在屏幕截图中称为 FortuneBuilders，因为那是我当时正在处理的项目的名称）会弹出项目设置对话框。在项目节点下方，你有一堆文件夹，其中一些是由 Xcode 为你创建的。iOS 开发人员熟悉的一件事是，Xcode 中的文件夹结构不一定与磁盘上的文件夹结构相匹配。位于 Classes 文件夹中的文件通常与位于 Controllers 目录中的文件一起坐在主项目目录中。这经常让熟悉 Visual Studio 的开发人员感到困惑，因为 Visual Studio 确实具有项目文件夹与磁盘文件夹之间 1:1 的映射。

![](img/04a00d46bb1059867d95707babd62ee7_72_0.png)

图 6.1 所示窗口的右侧是代码编辑器。在此窗口顶部，有时会出现一个单独的导航窗格，我已通过使用 Shift+Command+E 宏将其隐藏。配色方案是我个人偏好，而不是 Xcode 默认设置。因为开发人员通常对 IDE 中的语法高亮颜色非常挑剔，所以我想让你看到 Xcode 可以被制作成模仿几乎任何开发人员最喜欢的颜色和字体。

如果你好奇的话，屏幕截图中你看到的代码来自一个表视图控制器，该控制器显示通过访问特定 YouTube 用户上传视频的 Google 数据源下载的 YouTube 视频列表。屏幕截图中的代码显示了一些用于打开 Google 数据源信息并填充从 Interface Builder 文件加载的自定义表视图单元所需的代码。我们将在下一章讨论 Interface Builder 和 Microsoft 的设计工具 Expression Blend。

当你想运行应用程序时，你可以选择希望应用程序运行的环境。你可以选择 Debug 或 Release 模式，应用程序将在设备上运行还是在模拟器中运行，甚至在哪个特定基础 SDK 下运行应用程序。这给了你极大的灵活性，可以快速轻松地在你计划支持的所有可能环境下运行应用程序。图 6.2 显示了在 iOS 4.0 模拟器下运行应用程序时的样子。

![](img/04a00d46bb1059867d95707babd62ee7_73_0.png)

图 6.2 在 iOS 4 模拟器中运行的 iOS 应用程序。

