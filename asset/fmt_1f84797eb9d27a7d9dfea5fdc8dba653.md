
没有像 VB6 中旧式控件数组那样的 `Index` 属性。相反，只需使用事件处理程序的 `Sender` 参数来确定哪个控件引发了事件。

一个简单的示例有助于了解如何设置它。创建一个新的 Windows 应用程序并将空白 `Form1` 的 `Text` 属性设置为 `Add Dynamic Control Demo`。然后添加两个按钮到窗体，如图 14-26 所示。

![](img/d99870e80390742f93963da7be0b2e61_582_0.png)

双击 `Button1` 以切换到处理 `Button1.Click` 事件的代码。为了使此方法也响应 `Button2.Click` 事件，只需将 `Button2.Click` 事件处理程序添加到 `Handles` 列表的末尾，然后添加一些简单的代码来显示消息框，指示哪个按钮触发了事件：

```
' Note the change in the method name from Button1_Click. Since
' two objects are hooked up, it’s a good idea to avoid having the
' method specifically named to a single object.
Private Sub Button_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles Button1.Click, Button2.Click
Dim buttonClicked As Button
buttonClicked = CType(sender, Button)
' Tell the world what button was clicked
MessageBox.Show("You clicked " & buttonClicked.Text)
End Sub
```

来自 `AddDynamicControl` 的代码片段

运行程序并单击两个按钮。每个按钮都会触发事件并显示一个消息框，其中包含被单击按钮的适当文本。

### 运行时添加控件

你可以在运行时向窗体添加控件。以下示例增强了前面的程序，以在运行时动态添加第三个按钮。将另一个按钮添加到你的窗体，该按钮将触发 `Button3` 的添加，如图 14-27 所示。

![](img/d99870e80390742f93963da7be0b2e61_582_1.png)

将新按钮命名为 `AddNewButton` 并添加以下代码以处理其 `Click` 事件：

```
Private Sub AddNewButton_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) _
    Handles addNewButton.Click
Dim newButton As Button
' Create the new control
newButton = New Button()
' Set it up on the form
newButton.Location = New System.Drawing.Point(184, 12)
newButton.Size = New System.Drawing.Size(75, 23)
newButton.Text = "Button3"
' Add it to the form’s controls collection
```

`Me.Controls.Add(newButton)`
`' 挂钩事件处理程序。`
`AddHandler newButton.Click, AddressOf Me.Button_Click`
`End Sub`

来自 `AddDynamicControl` 的代码片段

当单击 `AddNewButton` 按钮时，代码会创建一个新按钮，设置其大小和位置，然后执行两个关键操作。首先，它将按钮添加到窗体的控件集合中；其次，它将按钮的 `Click` 事件连接到处理该事件的方法。

完成此操作后，运行程序并单击 `AddNewButton` 按钮。`Button3` 将出现。然后，只需单击 `Button3` 即可验证 `Click` 事件正在被处理。您应该会得到如图 14-28 所示的结果。

![](img/d99870e80390742f93963da7be0b2e61_583_0.png)

图 14-28

### 其他实用编程技巧

以下是一些使用 Windows Forms 的其他实用编程技巧：

- 将焦点切换到控件 — 使用 `.Focus` 方法。例如，要将焦点设置到 `TextBox1`，请使用以下代码：
  `TextBox1.Focus()`

- 快速确定容器控件或父窗体 — 由于使用了分组框和面板，控件通常被多层包含。您现在可以使用 `FindForm` 方法立即获取对窗体的引用。使用 `GetContainerControl` 方法可以访问控件的直接父级。

- 遍历 Tab 键顺序 — 使用任意控件的 `GetNextControl` 方法获取窗体上 Tab 键顺序中下一个控件的引用。

- 将客户端坐标转换为屏幕坐标（以及反向转换） — 想知道控件在屏幕坐标中的位置吗？使用 `PointToScreen` 方法。使用 `PointToClient` 方法转换回来。

- 在运行时更改控件的 Z 顺序 — 控件现在同时具有 `BringToFront` 和 `SendToBack` 方法。

- 定位鼠标指针 — `Control` 类现在公开了一个 `MousePosition` 属性，该属性返回鼠标在屏幕坐标中的位置。

- 管理子控件 — 容器控件（例如分组框或面板）可以分别使用 `HasChildren` 属性和 `Controls` 集合来确定子控件的存在与否以及直接引用。

- 最大化、最小化或还原窗体 — 使用窗体的 `WindowState` 属性。

- 创建全局异常处理程序 — 在“项目属性”对话框中，单击标记为“查看应用程序事件”的按钮。（仅当选中“使用应用程序框架”复选框时，此按钮才可用。）将创建一个名为 `ApplicationEvents.vb` 的新代码模块，您可以在该模块中处理 `UnhandledException` 事件。其他代码中未处理的任何异常都会触发此事件。

## 摘要

Windows Forms 仍然是开发富客户端和智能客户端界面的绝佳技术。虽然 Windows Presentation Foundation 在 .NET 平台的未来几代中将会经历更多创新，但目前使用 Windows Forms 开发要容易得多。Windows Forms 中设计器和控件集的成熟性使其成为许多基于客户端的应用程序的不错选择，并且 Windows Forms 将在 .NET 平台上得到无限期支持。

要成为一名熟练的 Windows Forms 开发人员，需要熟悉可用的控件，包括它们的属性、事件和方法。这需要时间。如果您对基于窗体的界面缺乏经验，则可能会花费相当多的时间使用参考文档来查找所需的控件功能。然而，这项投资是值得的，因为这不仅能让您成为一名熟练的 Windows Forms 开发人员，而且许多概念还会延续到 WPF 中。

许多专业的 Windows Forms 开发人员需要做的不仅仅是创建窗体和布置控件。复杂的应用程序通常还需要创建新控件或增强内置控件。因此，下一章将讨论如何创建和修改 Windows Forms 控件，以及一些其他高级 Windows Forms 主题。

### 15

### 高级 Windows Forms

## 本章你将学到什么

- 如何继承现有的 Windows Forms 控件并根据自己的目的扩展它们
- 如何创建将多个控件组合成可重用界面的 `UserControl`
- 如何创建绘制自身界面的 Windows Forms 控件

上一章讨论了 Windows Forms 2.0 的基础知识。这些功能足以满足用 VB 2010 编写的系统的简单用户界面需求；但随着应用程序变得更大、更复杂，使用 .NET 环境的高级功能来更好地构建应用程序结构就变得更加重要。结构不良的大型系统往往包含冗余代码。重复的代码模式最终会在应用程序的多个地方以（略有不同的变体）形式被使用，这会产生许多不良副作用：开发时间更长、可靠性更低、调试和测试更困难，以及维护更艰难。

常常导致重复代码的需求示例包括：确保用户输入了字段、确保字段格式正确，以及确保数据库中的空字段得到正确处理。正确的面向对象设计可以封装此类功能，从而无需使用重复代码。利用 .NET 环境的完整面向对象功能，加上 Windows Forms 编程特有的其他功能，您可以组件化您的逻辑，使相同的代码能够在应用程序的多个地方使用。

本章讨论在 Windows Forms 应用程序中组件化代码的技术。在阅读本章之前，假定您已经阅读了第 2 章和第 3 章关于 .NET 中继承和其他面向对象技术的内容。

### 在视觉控件中封装逻辑

如上一章所示，Windows Forms 用户界面基于控件的使用。控件只是一种特殊类型的 .NET 类（就像窗体一样）。作为一个完全面向对象的编程环境，VB 2010 使您能够继承和扩展类，控件也不例外。因此，可以创建新控件来扩展内置控件的功能。

用于 Windows Forms 界面的控件有四个主要来源：

- 随 .NET Framework 打包的控件（本章中称为内置控件）
- 导入到 Windows Forms 中的现有 ActiveX 控件（第 30 章将简要讨论这些控件）
- 来自软件供应商的基于 .NET 的第三方控件
- 为特定项目或组织中的特定目的而创建的自定义控件

如果您可以使用前三个类别中的控件来构建应用程序，那就更好了。使用满足目的的预编写功能通常是个好主意。然而，本章假设您需要的不仅仅是这种预打包功能。

### Windows Forms 中的自定义控件

在 .NET 中，创建自定义 Windows Forms 控件有三种基本技术，对应于三种不同的起点。这一系列选项提供了灵活性，您可以选择一种在简单性和灵活性之间取得适当平衡的技术：

- 您可以从现有控件继承。
- 您可以构建复合控件（使用 `UserControl` 类作为起点）。
- 您可以从头编写控件（使用非常简单的 `Control` 类作为起点）。

这些选项大致按复杂度排序，从最简单到最复杂。让我们逐一了解，以便理解每种选项适用的场景。

### 从现有控件继承

最简单的技术是从一个已经开发完整的 Windows Forms 控件开始。创建一个新类来继承该现有控件。这个新类具有其继承的基类的所有功能，并且可以添加新逻辑以在该新类中创建附加功能，或者实际上覆盖父类的功能（如果允许）。

以下是一些可能适合扩展现有 Windows Forms 控件的典型场景：

- 用于输入美式日期的文本框
- 自动加载的列表框、组合框或数据网格
- 具有重置为未选中状态机制的 `ComboBox` 控件
- 当其达到最大值允许值的 80% 时生成特殊事件的 `NumericUpDown` 控件

这些场景中的每一个都从一个需要一些附加功能的现有控件开始。您的项目中需要此类功能的频率越高，将其封装在自定义控件中就越是明智。如果需要在特殊验证或编辑的文本框只在一个地方使用，那么创建继承控件可能就不太合理。在这种情况下，在窗体中添加一些逻辑来处理控件的事件并操作控件的属性和方法可能就足够了。

#### 构建复合控件

在某些情况下，单个现有控件无法提供所需的功能，但两个或更多现有控件的组合却可以。这种组合称为复合控件。以下是一些典型示例：

- 一组具有相关逻辑且始终一起使用的按钮（例如文件维护窗体上的“保存”、“删除”和“取消”按钮）

  - 一组文本框，用于保存姓名、地址和电话号码，并以特定方式对组合信息进行格式化和验证
  - 一组选项按钮，其公开的单一属性为所选选项

与继承控件一样，复合控件仅适用于需要在多个位置使用相同功能的情况。如果该功能只需使用一次，那么通常最好直接将相关控件放在窗体上，并在窗体中包含相应的逻辑。

Windows 窗体中的复合控件通常使用 `UserControl` 类作为基类来创建。不过，也可以使用其他类作为基类来创建复合控件，后面标题为“在其他控件中嵌入控件”的一节将展示一个示例。

### 从头编写控件

如果某个控件需要现有控件中不具备的特殊功能，则可以从头编写该控件，以绘制自己的可视化界面并实现自己的逻辑。此选项需要更多工作，但使您能够在 .NET 和 Windows 窗体中实现几乎任何功能，包括非常复杂的用户界面。

要从头编写控件，必须继承 `Control` 类，该类提供基本功能，如颜色和大小属性。由于这些基本功能已内置，您需要完成的开发任务包括：为控件添加所需的任何特定属性和方法，编写将控件绘制到屏幕的渲染逻辑，以及处理鼠标和键盘输入。

### 从现有控件继承

在了解了创建自定义控件的这些选项之后，下一步是深入研究用于开发自定义控件的过程。首先是继承现有控件并扩展其新功能来创建自定义控件。这是创建新控件最简单的方法，也是介绍适用于所有自定义控件的通用技术的最佳方式。

在了解了通过继承创建自定义控件所需的一般步骤之后，一个示例将说明细节。务必理解，许多针对通过继承创建的控件所描述的技术也适用于创建控件的其他方式。无论继承自 `Control` 类、`UserControl` 类还是现有控件，控件都是 .NET 类。无论起点如何，创建属性、方法和事件，以及将这些成员与 Visual Studio 设计器协调起来，都是以类似方式完成的。

#### 流程概述

以下是通过继承现有控件来创建自定义控件所涉及的一般阶段。这不是一个逐步的配方，只是一个概述。后面的示例将提供有关具体步骤的更多细节，但这些步骤遵循这些基本阶段：

1. 创建或打开一个“Windows 控件库”项目，并向项目中添加一个新的自定义控件。创建的类将继承自 `System.Windows.Forms.Control` 基类。必须将指定继承类的行更改为继承自用作起点的控件。
2. 根据需要向类文件添加新逻辑，以增加新功能。然后使用“生成”操作编译项目，以创建包含新控件代码的 DLL。
3. 现在可以使用该控件了。在 Visual Studio 2010 中，可以使用“选择项”选项将其放入 Windows 窗体工具箱。此后，它可以像任何其他控件一样被拖到窗体上。

当然，第 2 阶段是工作量所在。自定义控件的新逻辑可能包括新的属性、方法和事件。也可能包括拦截基控件的事件并根据需要采取特殊操作。这些任务是使用标准的 .NET 编码技术完成的。

有几种编码技术是专门用于开发 Windows 窗体控件的，例如使用特定的 .NET 特性。虽然我们的示例包括添加常规属性和事件，但我们重点介绍这些用于控件编程的特殊技术。

#### 为继承的控件编写代码

本节讨论如何将新逻辑放入继承的控件中，并特别强调超越基本面向对象的技术。本节后面将提供一个使用这些技术的详细示例。

#### 为自定义控件创建属性

为自定义控件创建属性与为任何其他类创建属性类似。需要编写属性过程，并将属性值存储在某个位置，最常见的是存储在模块级变量中，该变量通常称为后备字段。

属性通常需要一个默认值——即控件实例化时属性自动采用的值。通常，这意味着将保存属性值的后备字段设置为某个初始值。这可以在声明后备字段时完成，也可以在控件的构造函数中完成。

下面是一个典型的自定义控件简单属性的代码：

```
Dim _nMaxItemsSelected As Integer = 10
Public Property MaxItemsSelected() As Integer
    Get
        Return _nMaxItemsSelected
    End Get
    Set(ByVal Value As Integer)
        If Value < 0 Then
            Throw New ArgumentException("property value cannot be negative")
        Else
            _nMaxItemsSelected = Value
        End If
    End Set
End Property
```

来自 `LimitedCheckedListBox` 的代码片段

为控件创建属性后，该属性会自动显示在控件的“属性”窗口中。如果“属性”窗口按字母顺序排列，您将在列表中看到它。如果窗口按类别排列，则新属性将出现在“杂项”类别中。但是，您可以使用一些附加功能来使该属性更好地与 Visual Studio 中的设计器和“属性”窗口配合。

#### 与 Visual Studio IDE 协调

控件通常被拖到由 Visual Studio IDE 管理的可视化设计图面上。为了使控件能够有效地与 IDE 配合，它必须能够指示其属性的默认值。IDE 需要属性的默认值来实现两个重要功能：

- 重置属性值（当用户在“属性”窗口中右键单击属性并选择“重置”时完成）
- 确定是否在设计器生成的代码中设置该属性。处于默认值的属性不需要在设计器生成的代码中显式设置。

您的控件可以通过两种方式与 IDE 配合来完成这些任务。对于采用简单值（如整数、布尔值、浮点数或字符串）的属性，.NET 提供了一个特性。对于采用复杂类型（如结构、枚举类型或对象引用）的属性，则需要实现两个方法。

#### 特性

您可以在第 4 章中了解有关特性的更多信息，但这里包含了要点的简短总结。特性与组件一样驻留在命名空间中。本章使用的特性位于 `System.ComponentModel` 命名空间中。要使用特性，项目必须引用包含特性命名空间的程序集。对于 `System.ComponentModel`，这没有问题——项目会自动引用。

但是，项目不会自动具有该命名空间的 Imports 语句。可以使用完整的类型名称来引用特性，但这有点笨拙。为了便于在代码中引用特性，请将以下行放在需要使用本章讨论的特性的所有模块的开头：

```
Imports System.ComponentModel
```

这样，只需使用名称即可引用特性。例如，下面详细讨论的 `DefaultValue` 特性可以这样声明：

```
<DefaultValue(4)> Public Property MyProperty() As Integer
```
