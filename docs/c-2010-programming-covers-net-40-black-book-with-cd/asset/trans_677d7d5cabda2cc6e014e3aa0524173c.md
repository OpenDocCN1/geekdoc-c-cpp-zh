

## 摘要

在本章中，你学习了 Windows Forms 以及如何在其上执行各种操作，例如添加控件、禁用和启用 Windows 窗体、更改 Windows 窗体的标题、设置 Windows 窗体的边框，以及隐藏和显示 Windows 窗体的最大化、最小化和关闭按钮。接下来，你学习了如何在 Windows 应用程序中创建多个窗体。此外，你还学习了如何设置控件和窗体的不同属性。最后，本章描述了如何处理鼠标和键盘事件。

本章提供了 Windows Forms 及其控件的概述。本书随附的光盘包含五章附赠内容，提供 Windows Forms 控件更详细和深入的描述：

- 附赠章节 1 描述了 Button、Label、TextBox、RichTextBox 和 MaskedTextBox 控件
- 附赠章节 2 描述了 RadioButton、CheckBox、ListBox、CheckedListBox 和 ComboBox 控件
- 附赠章节 3 涵盖了 ListView、TreeView、ImageList、PictureBox、Panel、GroupBox 和 TabControl 控件
- 附赠章节 4 阐述了 SplitContainer、ScrollBar、TrackBar、ToolTip、NotifyIcon、MonthCalendar、DateTimePicker、Timer 和 ProgressBar 控件
- 附赠章节 5 描述了 ToolStrip、MenuStrip、ContextMenuStrip、StatusStrip 和对话框控件

在下一章中，你将学习 Windows Presentation Foundation (WPF) 的基础知识。

## 9

## 介绍 Windows Presentation Foundation

| 如果你需要立即解决的问题： | 请参阅页码： |
|---|---|
| 使用 WPF 窗口 | 354 |
| 通过 XAML 向网格添加行和列 | 359 |
| 在 WPF 4.0 应用程序中创建对话框 | 361 |
| 使用自定义路由事件 | 364 |

![](img/e073a4882197be4ab61103cbe0bcb394_340_0.png)

## 深入探讨

到目前为止，你已经学习了使用 Windows Forms 开发桌面应用程序。Visual Studio 2010 包含另一种技术，即 Windows Presentation Foundation (WPF)，用于开发桌面应用程序。WPF，之前称为 Avalon，为开发高端桌面应用程序提供了多种功能和特性。它支持各种媒体，如文本、图像、音频、视频，并允许你使用二维 (2-D) 以及三维 (3-D) 图形。正如你所知，Windows Forms 需要众多技术来处理 2-D、3-D 和多媒体。一些技术示例包括：GDI+、Windows Media Player 应用程序编程接口 (APIs) 和 DirectX APIs。与 Windows Forms 不同，WPF 本身就提供了这些技术，因此你无需在 WPF 中使用单独的 API 来处理图形、动画和多媒体。因此，使用 WPF 开发图形丰富的桌面应用程序更容易、更简单。WPF 应用程序中的所有设计相关元素均由 DirectX 处理。

与 Windows Forms 类似，WPF 也适用于用户界面 (UI) 设计师和应用程序开发人员。它为设计师和开发人员提供了一个便捷的平台，以便他们共享和协作工作以完成任务。WPF 最初随 .NET Framework 3.0 引入，包含在 .NET Framework 3.5 和 4.0 中。.NET Framework 4.0 中包含的 WPF 版本是 WPF 4.0。WPF 还支持可扩展应用程序标记语言 (XAML)。XAML 是由 Microsoft Corporation 引入的基于可扩展标记语言 (XML) 的声明性标记语言。此标记语言允许设计师轻松、快速地定义和描述 WPF 应用程序 UI 的元素。之后，应用程序开发人员可以使用 XAML 定义的 UI 元素在代码隐藏文件中用 C# 等 .NET 语言指定应用程序逻辑。此外，你还可以使用代码隐藏文件在运行时创建 UI 元素。因此，WPF 允许在 WPF 应用程序中对 UI 方面和应用程序逻辑进行分离和集成。

在本章中，你将学习 WPF 4.0 的新特性和基本概念，例如其架构、类层次结构和应用程序模型。本章还解释了如何创建和执行 WPF 4.0 应用程序。此外，本章描述了 WPF 4.0 设计器、XAML 基础、WPF 属性和事件，以及 WPF 对话框。

让我们先讨论 WPF 4.0 的新特性。

## WPF 4.0 的新特性

WPF 是一个 UI 框架，可帮助你创建交互式客户端应用程序。它支持各种应用程序开发功能，例如控件、图形、布局和数据绑定。WPF 使用 XAML 语言进行应用程序编程。你可以使用 WPF 创建独立和浏览器托管的应用程序。

WPF 4.0 相较于其前一版本 WPF 3.5 有多项改进和增强。WPF 4.0 的一些新特性包括：

- 用于开发业务应用程序的新 WPF 控件
- 支持触控启用应用程序的开发
- 用于增强动画的缓动函数
- Visual State Manager (VSM)
- 选择和插入符号画刷
- 新的 WPF 文本渲染堆栈
- 对 XAML 浏览器应用程序 (XBAPs) 的改进

让我们详细探讨 WPF 4.0 的这些特性。

## 新的 WPF 控件

在 WPF 4.0 中，添加了三个新控件：DataGrid、Calendar 和 DatePicker，用于开发业务应用程序。这些控件使你能够重用应用程序的代码并创建丰富的客户端和 Web 应用程序。让我们在下一节中简要介绍这些控件。

## DataGrid

DataGrid 是一个控件，以网格格式显示数据库表中的数据。它以行和列的形式显示数据。此外，它会根据存储在其中的数据类型自动生成列，通过设置 ItemsSource 属性。你可以对 DataGrid 控件中存储的数据执行各种操作，例如分组、排序和筛选。此外，DataGrid 控件使你能够在单元格和行级别执行验证。在单元格级别验证时，你可以在另一用户更新值时验证绑定数据对象 (单元格) 的属性。然而，在行级别验证时，你可以在另一用户修改行中的数据时验证整个数据对象 (行)。

> NOTE
> 要了解有关 DataGrid 控件的更多信息，请参阅第 25 章《Windows Forms 和 WPF 应用程序中的数据绑定》。

## Calendar 控件

Calendar 是一个控件，允许你从可视日历中选择日期。它可以作为单独的控件使用，也可以作为 DatePicker 控件的下拉部分。图 9.1 显示了 WPF 应用程序 MainWindow 中的 Calendar 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_342_0.png)

图 9.1：在 MainWindow 中显示 Calendar 控件

> NOTE
> 要了解有关 Calendar 控件的更多信息，请参阅第 12 章《在 Windows Forms 和 WPF 中使用图形和多媒体》。

## DatePicker

DatePicker 是一个控件，允许你通过在文本字段中输入日期或使用下拉 Calendar 控件来选择日期。图 9.2 显示了 WPF 应用程序 MainWindow 中的 DatePicker 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_342_1.png)

图 9.2：在 MainWindow 中显示 DatePicker 控件

![](img/e073a4882197be4ab61103cbe0bcb394_344_0.png)

## 图 9.3：显示按钮控件的不同状态

ControlTemplate 是一个类，用于指定控件的视觉结构和行为方面，以便这些方面可以在控件的多个实例之间共享。VisualStateManager 类使你能够为控件指定不同的状态以及控件的外观。

## 选择和插入符号画刷

在 WPF 4.0 中，添加了两个新的画刷，Selection 和 Caret，用于突出显示选定文本和绘制光标。这些画刷在输入和阅读控件上工作，例如 TextBox、RichTextBox 和 FlowDocumentReader。这些画刷以 TextBoxBase 类的属性形式存在。这些属性如下：

- SelectionBrush – 创建一个画刷以突出显示选定文本
- CaretBrush – 创建一个画刷以绘制光标

TextBoxBase.SelectionBrush 和 TextBoxBase.CaretBrush 属性属于 System.Windows.Controls.Primitives 命名空间。以下是这些属性的语法：

```
public Brush SelectionBrush { get; set; }
public Brush CaretBrush { get; set; }
```

以下代码片段显示了使用 SelectionBrush 的示例：

```
<TextBox SelectionBrush="Yellow" SelectionOpacity="0.8" Foreground="Green">
You are using the SelectionBrush and CaretBrush properties.
</TextBox>
```

前面的代码片段创建一个文本框并向其中添加文本，You are using the SelectionBrush and CaretBrush properties。我们已将 SelectionBrush 属性指定为黄色。注意，还有另一个属性 SelectionOpacity，设置为 0.8 以自定义选定文本的外观。图 9.4 显示了 SelectionBrush 属性的使用：

![](img/e073a4882197be4ab61103cbe0bcb394_344_1.png)

## 图 9.4：使用 SelectionBrush 属性显示高亮文本

以下代码片段显示了使用 CaretBrush 属性的示例：

```
<TextBox Foreground="Green" CaretBrush="Red">
You are using the SelectionBrush and CaretBrush properties.
</TextBox>
```

前面的代码片段创建一个文本框并向其中添加文本，You are using the SelectionBrush and CaretBrush properties。我们已将 CaretBrush 属性指定为红色，将 Foreground 属性指定为绿色。图 9.5 显示了 CaretBrush 属性的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_344_2.png)

## 图 9.5：使用 CaretBrush 属性显示红色光标

你可以在 SelectionCaretBrushesUse 应用程序（可在光盘中找到）中找到使用 SelectionBrush 和 CaretBrush 属性的代码。

