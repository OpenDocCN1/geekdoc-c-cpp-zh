

这个技术最好通过一个示例来呈现。标准的 ComboBox 控件没有让用户重置为“无选择”状态的方法。一旦选择了项目，将其设置为该状态需要代码将 SelectedIndex 设置为 -1。

本练习创建一个 ComboBox，该 ComboBox 具有一个按钮，可将选择状态重置回“无选择”。这使用户可以直接访问该功能。现在你已经在示例中处理了多个控件，而不是逐步进行，我们将直接展示此类 ComboBox 的代码并讨论代码的工作原理：

```
Public Class SpecialComboBox
    Inherits ComboBox
    Dim WithEvents btnEmbeddedButton As Button
    Public Sub New()
        Me.DropDownStyle = ComboBoxStyle.DropDownList
        ' Fix up the embedded button.
        btnEmbeddedButton = New Button
        btnEmbeddedButton.Width = SystemInformation.VerticalScrollBarWidth
        btnEmbeddedButton.Top = 0
        btnEmbeddedButton.Height = Me.Height - 4
        btnEmbeddedButton.BackColor = SystemColors.Control
        btnEmbeddedButton.FlatStyle = FlatStyle.Popup
        btnEmbeddedButton.Text = "*"
        Dim fSpecial As New Font("Wingdings 3", Me.Font.Size - 1)
        btnEmbeddedButton.Font = fSpecial
        btnEmbeddedButton.Left = Me.Width - btnEmbeddedButton.Width - SystemInformation.VerticalScrollBarWidth
        Me.Controls.Add(btnEmbeddedButton)
        btnEmbeddedButton.Anchor = CType(AnchorStyles.Right Or AnchorStyles.Top Or AnchorStyles.Bottom, AnchorStyles)
        btnEmbeddedButton.BringToFront()
    End Sub

    Private Sub btnEmbeddedButton_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles btnEmbeddedButton.Click
        Me.SelectedIndex = -1
        Me.Focus
    End Sub
    Private Sub BilllysComboBox_DropDownStyleChanged(ByVal sender As Object, ByVal e As System.EventArgs) Handles MyBase.DropDownStyleChanged
        If Me.DropDownStyle <> ComboBoxStyle.DropDownList Then
            Me.DropDownStyle = ComboBoxStyle.DropDownList
            Throw New InvalidOperationException("DropDownStyle must be DropDownList")
        End If
    End Sub
End Class
$$

```

来自 SpecialCombo 的代码片段

与本章中的第一个示例一样，此示例继承自内置控件。因此，它立即获得了标准 ComboBox 的所有功能。你需要添加的只是重置所选状态的能力。

为此，你需要一个供用户按下的按钮。类将按钮声明为名为 btnEmbeddedButton 的私有对象。然后，在类的构造函数中，实例化按钮，并根据需要设置其属性。按钮的大小和位置需要计算。这使用 ComboBox 的大小和一个名为 SystemInformation.VerticalScrollBarWidth 的特殊系统参数来完成。该参数被选中，因为它也用于计算用于下拉组合框的按钮的大小。因此，你的新嵌入按钮的宽度将与常规 ComboBox 显示用于下拉列表的按钮的宽度相同。

当然，你需要在新按钮中显示一些内容以指示其用途。为简单起见，前面的代码使用 WingDings 3 字体显示一个小写的“t”（所有 Windows 系统都应已安装该字体）。这会导致出现左指向三角形，如图 15-9 所示，该图是控件使用中的屏幕截图。

然后按钮被添加到 ComboBox 的 Controls 集合中。你可能会惊讶地发现 ComboBox 甚至有一个用于嵌入控件的 Controls 集合，但 Windows Forms 中的所有控件都有一个。

最后，设置新按钮的 Anchor 属性以在 SpecialComboBox 被其使用者调整大小时保持位置。

除了构造函数之外，只需要几个小的例程。必须处理按钮的 Click 事件，在其中将 SelectedIndex 设置为 -1。此外，由于此功能仅适用于样式为 DropDownList 的组合框，因此必须捕获 ComboBox 的 DropDownStyleChanged 事件，并防止样式被设置为其他任何内容。

![](img/d99870e80390742f93963da7be0b2e61_607_0.png)

## SUMMARY

本章讨论了如何在 Windows Forms 中创建自定义控件，从而能够在用户界面中整合使用的逻辑。.NET 中的完整继承功能和 Windows Forms 命名空间中的类为创建控件提供了多种选择。最好先通过覆盖这些控件来学习创建属性的基础知识以及它们与设计器的协调、构建控件和测试它们等。这些技术随后可以通过创建复合控件来扩展，正如本章中的示例所说明的那样。

我们还讨论了从头开始创建控件，使用基类 Control。在编写从头开始的控件的过程中，有必要讨论 GDI+ 的基础知识，但如果你要进行大量的 GDI+ 工作，你需要寻找额外的资源来帮助这项工作。

你应从本章带走的关键概念是，Windows Forms 控件既是打包将在许多窗体中重用的功能的好方法，也是以更少的代码更快地创建更动态、更响应式的用户界面的好方法。

## 16

## User Controls Combining WPF and Windows Forms

### WHAT YOU WILL LEARN IN THIS CHAPTER

- The Windows Forms Integration Library
- Using WPF controls in Windows Forms
- Using Windows Forms controls in WPF
- Integration library limitations

第 15 章介绍了 Windows Forms 的高级功能。其中一个功能远远超出了 Windows Forms：用户控件。用户控件用于 Windows Forms、ASP.NET、WPF 和 Silverlight。围绕用户控件的概念反映了将应用程序逻辑封装在可重用组件中的最佳实践。在应用程序内部，较小的组件封装功能并通过事件等方法进行通信，提供了一个强大的架构。本章作为通往下一章的桥梁，该章涉及 WPF，也引用了使用用户控件。

相同的概念被用来提供从 Windows Forms 到 Windows Presentation Foundation（WPF）的迁移路径。WPF 最初在 .NET 3.0 中引入，是微软面向图形用户界面开发的下一代解决方案。就用户界面而言，过渡到这种新模型的重要性以及范式转变将类似于从基于 COM 的 Visual Basic 到 Visual Basic .NET 的转变。熟悉 Windows 应用程序开发人员的核心范式和语法正在发生变化，而且大多数变化都不向后兼容。

因此，开发人员需要将现有的应用程序源代码迁移到新的技术范式。也许不是今年或明年，但在某个时候，WPF 范式将被用来更新现有应用程序的外观和感觉。这种过渡将与上一次主要的 .NET 相关过渡——从 COM 的过渡——相比如何？Visual Studio .NET 的原始版本包含一个工具，用于帮助将代码从基于 COM 的世界迁移到 .NET。不会提供迁移工具来将现有用户界面过渡到 WPF，这应该被认为是一件好事，考虑到当前迁移工具的历史。

相反，微软吸取了迁移既困难又耗时的教训，最好由开发人员自行决定节奏。因此，而不是尝试自动处理基于过程范式的代码以在声明性范式下工作，选择的工具是使在各自范式下构建的组件能够通信的工具。毕竟，在某些情况下，这种更改会导致应用程序或应用程序 UI 的完全重写，而迁移库永远不会被使用。

这种相同的互操作范式在 Visual Basic 的 Power Pack 工具中重复出现，微软于 2006 年首次发布了这些工具。这些工具的概念与微软为 WPF 选择的 Interop 方法论相似，涵盖在附录 B 中。

微软提供了库，使用户界面开发人员能够集成这两个用户界面模型（WPF 和 Windows Forms）。从长远来看，Windows Forms 到 WPF 的集成可能会像 COM-Interop 一样发展，这意味着它将可用多年，但其局限性和与旧技术的联系将降低其影响力，最终它将与旧技术一起被迫退休。

本章的重点是如何使用 Windows Forms Integration Library 来最好地让你既能利用 WPF 与现有代码，又能利用现有代码和相关窗体代码与新的 WPF 应用程序一起使用。就像 COM-Interop 一样，集成库的目的是帮助你，开发人员，逐步将应用程序从 Windows Forms 迁移到 WPF，同时处理所有开发人员面临的时间和预算限制，并可能等待 WPF 中不可用的控件。

## THE INTEGRATION LIBRARY

WindowsFormsIntegration 库使 WPF 应用程序能够托管 Windows Forms 控件，反之亦然。该库包含在 WindowFormsIntegration.dll 中，支持 System.Windows.Forms.Integration 命名空间。该命名空间提供了在单个应用程序中使用 WPF 和 Windows Forms 所需的工具。该命名空间的核心是两个类 ElementHost 和 WindowsFormsHost。这两个类分别提供了 WPF 和 Windows Forms 环境中的互操作性。

WindowsFormsIntegration.dll 位于其他 .NET 程序集旁边，并像任何其他通用命名空间一样导入。在添加引用并导入命名空间后，你会发现适用于你的项目类型的适当控件类——ElementHost 或 WindowsFormsHost——在设计器的工具箱窗口的工具列表中。

表 16-1 描述了构成 Windows.Forms.Integration 命名空间的类和委托，MSDN 上也有一个类似的列表：http://msdn.microsoft.com/en-us/library/system.windows.forms.integration.aspx。

## TABLE 16-1: Windows.Forms.Integration Classes and Delegate

| CLASS | DESCRIPTION |
|---|---|
| ChildChangedEventArgs | 此类在传递 ChildChanged 事件的参数时使用。此事件在 WindowsFormsHost 和 ElementHost 类上发生，当 Child 属性的内容发生变化时。 |
| ElementHost | 这是嵌入 WPF 控件到 Windows Forms 中的核心类。使用 Child 属性，你标识将被托管的顶级对象（可能是某种面板），并通过该对象定义将被该对象控制的区域。主机引用的对象可以包含其他控件，但主机仅引用这一个。 |
| IntegrationExceptionEventArgs | 这是 Integration 和 Property Mapping 异常类的基类。它提供了这些类使用的通用实现。 |
| LayoutExceptionEventArgs | 此类使你能够将与主机类中的布局错误相关信息返回到托管环境、Windows Forms 或 WPF。 |

