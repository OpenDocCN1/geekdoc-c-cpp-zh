

设置好应用程序的外观后，就该开始处理一些代码了。你会在下面的代码中注意到，默认目录再次是 Windows 7 上的 Images 目录。下一个方法是 Window1_Loaded 方法。该方法在窗体初始加载时调用一次，是创建自定义用户控件实例并将其分配为 WindowsFormsHost1 的子项的理想位置。此初始列表中还有一行被注释掉了；在第一次试运行应用程序后，你将取消注释该行。

两个按钮都需要事件处理程序。在这种情况下，你可以使用 Visual Basic Handles 子句将示例代码中显示的方法与按钮关联起来。Button1 和 Button2 在下面的代码片段中都有关联的处理程序。

此代码的大部分与 Button1_Click 事件处理程序相关。在此例中，为简洁起见，应用程序不会自动加载目录的内容。相反，当你第一次单击 Button1 时，你将被允许选择默认文件夹，然后加载该文件夹的内容。请注意，尽管网格是用两列创建的，但此示例代码仅为演示目的将文档名称加载到自定义用户控件的一部分的网格中：

```
Class MainWindow
    'Private Sub Window1_Initialized(ByVal sender As Object,
                    ByVal e As System.EventArgs) Handles Me.Initialized
        '    Me.WindowStyle = Windows.WindowStyle.None
        '    Me.AllowsTransparency = True
    'End Sub

    Private Sub Window1_Loaded(ByVal sender As System.Object,
                    ByVal e As System.Windows.RoutedEventArgs) Handles MyBase.Loaded
        WindowsFormsHost1.Child = New WinFormInteropCtrl.UserControl1()
        PopulateGrid("C:\Users\Public\Pictures\Sample Pictures")
        System.Windows.Forms.Application.EnableVisualStyles()
    End Sub

    Private Sub Button1_Click(ByVal sender As System.Object,
                    ByVal e As System.Windows.RoutedEventArgs) Handles Button1.Click
        Dim FolderBrowserDialog1 As New System.Windows.Forms.FolderBrowserDialog()
        FolderBrowserDialog1.SelectedPath = "C:\Users\Public\Pictures\Sample Pictures"
        If (FolderBrowserDialog1.ShowDialog() = Windows.Forms.DialogResult.OK) Then
            PopulateGrid(FolderBrowserDialog1.SelectedPath)
        End If
    End Sub

    Private Sub PopulateGrid(ByVal path As String)
        Dim uc As WinFormInteropCtrl.UserControl1 =
                    CType(WindowsFormsHost1.Child, WinFormInteropCtrl.UserControl1)
        Dim roid As Integer
        For Each control As System.Windows.Forms.Control In uc.Controls
            If TypeOf control Is System.Windows.Forms.DataGridView Then
                Dim grid As System.Windows.Forms.DataGridView = control
                grid.Rows.Clear()
                For Each filename As String In System.IO.Directory.GetFiles(path)
                    roid = grid.Rows.Add()
                    grid.Rows(roid).Cells(0).Value = filename
                    grid.Rows(roid).Cells(1).Value = New System.IO.FileInfo(filename).Length
                Next
            End If
        Next
    End Sub

    Private Sub Button2_Click(ByVal sender As System.Object,
                    ByVal e As System.Windows.RoutedEventArgs) Handles Button2.Click
        Me.Close()
```

```
End Sub
End Class
```

> 来自 MainWindow.xaml 的代码片段

最后，请注意，最后一个方法是 Button2.Click 事件的事件处理程序。正如你所预期的那样，此事件处理关闭窗口，这在你隐藏窗口外部框架时是一个重要的功能。

此时你可以运行应用程序。如果你使用的是可下载的包，你应该会看到图 16-6 所示的结果。如果你自己创建项目副本，你应该会看到类似的结果；但是，WindowsFormsHost1 中的按钮应具有不正确的样式。

![](img/d99870e80390742f93963da7be0b2e61_623_0.png)

首先映入眼帘的是，WinFormInteropCtrl 丢失了 Windows XP 视觉样式。参考回图 16-6，你可以确认该样式在该控件的设计器中存在。为了解决此问题，请转到 Window1.xaml 文件的代码隐藏文件 Window1.xaml.vb。在 Window1_Loaded 方法中，在创建用户控件作为控件 WindowsFormsHost1 的子项的调用之前或之后，添加以下代码行：

```
System.Windows.Forms.Application.EnableVisualStyles()
```

重新运行应用程序。视觉样式现在是正确的，但你也应该能够看到 WPF 和 Windows Forms 在类似控件上以不同的方式呈现此样式。因此，你需要确保尽量减少在主机边界两侧引用的类似控件的数量。在此例中，你只需手动重置控件的显示设置以指示它应使用 Windows XP 样式；但是，此样式问题为下一个主题提供了很好的介绍。

注意 Windows 7 用户可能会遇到额外的显示问题。出于某种原因，Windows 7 和 WPF Interop 库会导致显示问题。问题在窗口调整大小时会消失，但如果你看到幽灵图像，请调整正在运行的窗口的大小，它就会消失。此问题未在图 16-6 中显示。

上一章中讨论的关于 WPF 的选项之一是更改窗口样式的能力，以便隐藏框架中的传统边框和控件。完成此操作后，可以启用透明度并真正致力于为应用程序创建自定义的外观和感觉。然而，你会注意到以下代码在在线材料中被注释掉了。那是因为此代码用于说明 WindowsFormsHost 控件的局限性之一。

```
Private Sub Window1_Initialized(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles Me.Initialized
    Me.WindowStyle = Windows.WindowStyle.None
    Me.AllowsTransparency = True
End Sub
```

如果你启用此代码，你会发现 WPF 渲染引擎不会渲染任何内容，而不是让你的互操作控件显示。因此，虽然限制包括无法使用某些类型的透明度与控件一起使用，但这更能说明使用 WindowsFormsHost 控件如何影响应用程序的整体外观和感觉。

## INTEGRATION LIMITATIONS

集成的挑战在于这两种显示模型不在同一范式下运行。Windows Forms 世界和 WindowsFormsHost 基于窗口句柄，也称为 HWnd 结构。相比之下，WPF 仅有一个 HWnd 来为操作系统定义其显示区域，然后避免使用 HWnds。因此请记住，当你处理封装控件时，该控件——无论是 WPF 还是 Windows Forms——都会受到其所托管的环境的影响。

例如，如果你在 Windows Forms 应用程序中托管一个 WPF 控件，那么控制低级图形显示特征（如不透明度或背景）的能力将受到 Windows Forms 规则的限制。与 WPF 不同，WPF 在当前控件下方的一层支持控件特征以支持控件的显示，Windows Forms 控件包含在 HWnd 中；当 HWnd 没有为你的 WPF 控件绘制背景时，显示可能会将该区域显示为未绘制，并使用黑色或白色背景代替。请注意，设置控件的 AllowTransparency 属性在将 WPF 控件托管在 Windows 窗体上时是受支持的。你可以尝试为本章前面介绍的 ElementHost 控件使用的背景颜色，以感受此问题。

认识到主机控件通常受包含它的底层环境限制，是预测限制的一个良好指南。虽然有时父应用程序框架的实际特征可能会令人惊讶，但随着你对 WPF 的经验增加，你将能够预测问题可能存在的位置。例如，你可以创建基于窗口和基于页面的 WPF 应用程序，但这些应用程序在完全不同的模型上运行。例如，基于页面的 WPF 应用程序是无状态的。为了支持这种无状态特性，在那些在基于页面的 WPF 应用程序中使用它的情况下，WindowsFormsHost 控件在每次页面刷新时都会完全刷新包含的控件——丢失你可能期望保留在 Windows Forms 控件中的任何用户输入。

另一个问题可能与 WPF 的高级缩放功能有关。虽然 Windows Forms 控件是可缩放的，但 Windows Forms 不支持缩放至 0 然后正确恢复的概念。

同样，请注意托管控件的消息循环、当前控件焦点和属性映射。主机控件支持向它们包含的控件传递消息，但在应用程序范围内，消息的顺序可能不会按预期顺序发生。同样，当 WindowsFormsHost 控件已将焦点传递给包含的控件然后窗体被最小化时，主机控件可能无法跟踪其子项中哪个控件具有该焦点。因此，即使看不见的主机在你的 WPF 应用程序中具有当前焦点，也没有可见的控件具有该焦点。

最后，除了前面描述的背景颜色问题之外，还有其他潜在的属性映射问题，因此你需要仔细观察这些控件的行为，并准备好手动映射属性，如本章第一个示例所示。

这不是在尝试集成这两种不同的用户界面实现时可能遇到的潜在问题的完整列表。最后的警告是，你不能嵌套主机控件。Windows Forms 和 WPF 都可以在给定窗口中包含多个主机控件，但这些主机控件必须分开且类型相同。因此，你不能创建包含 WindowsFormsHost 控件的 WPF 应用程序，该控件包含 ElementHost 控件。如果你正在集成控件，请尽量减少包含主机控件的面板数量，以免意外尝试在另一层集成中嵌套嵌入的主机控件。

## SUMMARY

本章扩展了用户控件的覆盖范围，涉及如何利用它们在不同的显示系统之间封装应用程序逻辑。本章介绍了 Windows.Forms.Integration 库以及让 WPF 和 Windows Forms 组件提供应用程序用户界面的能力。此库类似于其他过渡库，其重点是支持业务需求，而不是在 WPF 环境中完全支持 Windows Forms 组件的 WPF 功能。本章的关键点如下：

- ► 可以使用 Windows.Forms.Integration 库和 ElementHost 类开始迁移到基于 WPF 的应用程序界面。
- ► 这样的界面使你能够将增强的图像处理嵌入到现有的 Windows Forms 应用程序中。

