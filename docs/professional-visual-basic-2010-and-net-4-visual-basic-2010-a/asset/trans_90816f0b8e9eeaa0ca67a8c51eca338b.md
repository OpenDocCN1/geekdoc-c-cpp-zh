

' whether margin is set or not. if the actual size is greater than the
' size of the image reset margins to the max size of the image.
Dim imgH As Double = image.Height
Dim ctrlH As Double = Me.ActualHeight
Dim marginHorizontal As Double
If imgH > ctrlH Then
    marginHorizontal = 0
Else
    marginHorizontal = (ctrlH - imgH) / 2
End If

Dim imgW As Double = image.Width
Dim ctrlW As Double = Me.ActualWidth
Dim marginSide As Double
If imgW > ctrlW Then
    marginSide = 0
Else
    marginSide = (ctrlW - imgW) / 2
End If
Image1.Margin = New Thickness(marginSide, marginHorizontal, marginSide, marginHorizontal)

End Sub
End Class

来自 UserControl1.xaml 的代码片段

其余的自定义代码实际上就是 ResizeMargins 方法。这个方法相当简单。它获取图像本身的大小，并将其与 Image1 控件的大小进行比较。请注意，这段代码引用了 ActualHeight 属性。与 Height 属性（对于停靠的控件，该属性不能提供有效大小）不同，ActualHeight 属性反映的是 Image1 控件的当前大小。如果控件大小大于图像的原始大小，代码就会调整边距，以便在图像周围填充空白。

至此，示例 WPF 控件库的定义就完成了，因此请编译应用程序，确保没有遗留错误。

## Windows 窗体应用程序

下一步是自定义 Windows 窗体应用程序。首先添加五个必要的引用，以便能够嵌入并操作此控件。它们分别是四个框架库——WindowsFormsIntegration、PresentationCore、PresentationFramework 和 WindowsBase——以及对自定义 WpfInteropCtrl 库的项目引用。打开 ProVBWinForm_Interop 项目的项目属性，转到“引用”选项卡。

选择“添加引用”，在可用 .NET 库列表中，你会找到所有四个框架引用。此屏幕上还提供了其他演示库；你可以根据在应用程序中要做的事情，选择向项目添加其他库引用。最后，切换到“项目引用”选项卡，并添加对本地项目的引用。

### 在窗体上布局控件

现在进入 Form1.vb 文件的设计模式。该文件是你在创建此项目时由 Windows 窗体模板生成的。在扩展设计图面的默认大小时，要考虑控件的大小，为在自定义用户控件上方排列三行 Windows 窗体控件留出足够的空间。

从顶部开始，你将在窗体的左上角添加一个新的 Button 控件。此按钮上的标签为“选择文件夹”；要更改此标签，你需要更新控件的 Text 属性。确保按钮的大小足以完整显示其文本。接下来，向窗口中添加一个 FolderBrowserDialog 控件；此控件没有显示元素，它将显示在窗体下方。现在，在按钮下方添加一个 Label 控件，并将其 Text 属性更改为“图像..”。放置好之后，在此标签的右侧添加一个 ComboBox 控件。保留默认名称 ComboBox1，并在控件的属性中选择 Anchor 属性，除了默认的顶部和左侧锚定外，再将控件的右侧锚定到容器。这会使控件随着包含它的窗体变宽而扩展。

接下来，在按钮右侧添加一个 Label 控件，使用文本“遮罩：”。在“遮罩：”标签的右侧，按照示例代码添加一个新的组合框 ComboBox2。转到此 ComboBox 的上下文菜单，选择“编辑项”以打开编辑窗口。在此界面中，添加构成图像遮罩选项的三个选项：无遮罩、椭圆和矩形。确保此控件也锚定到窗体的宽度。

在图像 ComboBox 下方、窗体的第三行中，添加一个文本为“边距：”的 Label 控件，以及一个名为 TextBoxMargin 的 TextBox 控件。在属性窗口中，将此 TextBox 的默认值设置为 10，并将其长度限制为 4 个字符。同样，在此文本框旁边，添加另一个文本为“圆角半径：”的 Label 控件，以及一个名为 TextBoxRounding 的第二个 TextBox 控件。将这个第二个文本框的默认值设置为 50。

此时，将你的 UserControl1 直接拖放到窗体图面上。这是与 Visual Studio 2008 相比的一个变化。在 Visual Studio 2010 中，你将目标 WPF 控件拖到窗体上，设计器会自动使用 ElementHost 控件封装该 WPF 控件。然后，你可以调整 ElementHost 的大小以填充可用区域，并使用 ElementHost 的 Anchor 属性将其锚定到四个边，以确保它随窗体一起调整大小。

Form1 的设计视图应类似于图 16-2 所示。注意展开的“属性”窗格。当前它被设置为显示/编辑 ElementHost1 的属性，并聚焦于其对用户控件的引用。

![](img/d99870e80390742f93963da7be0b2e61_614_0.png)

# 图 16-2

### 向窗体添加自定义代码

下一步是向此窗体添加一些自定义代码。该窗体将允许你选择一个包含图像的文件夹，然后显示其中任意图像。此外，你将能够在图像上放置一个遮罩，为显示的图像提供自定义“边框”。该示例的目的不仅是演示添加控件，还演示一种需要在代码中映射 ElementHost 的某个属性的场景。

下面的代码清单提供了自定义的基础。第一项是保存当前目录路径。该私有值定义在窗体类上，并为该属性分配了一个 Windows 7 上的默认图像路径。接下来，处理窗体的 Load 事件。在 Load 事件中，代码将获取默认目录中的文件列表，然后用此列表填充 ComboBox1。它将从列表中选择第一个文件，然后确保未选择任何遮罩。最后，示例代码调用 AddPropertyMapping 方法。此调用当前处于注释状态，待说明属性映射的原因后，再取消注释。

```
Public Class Form1
    ' The default directory path is native to Windows 7.
    ' On other operating systems select an appropriate directory.
    Private m_path As String = "C:\Users\Public\Pictures\Sample Pictures"
    Private Sub Form1_Load(ByVal sender As System.Object, _
                           ByVal e As System.EventArgs) _
                           Handles MyBase.Load
        For Each filename As String In System.IO.Directory.GetFiles(m_path)
            ComboBox1.Items.Add(filename)
        Next
        ComboBox1.SelectedIndex = 0
        Me.ComboBox2.SelectedIndex = 0
        'AddPropertyMapping()
    End Sub
    Private Sub Button1_Click(ByVal sender As System.Object, _
                              ByVal e As System.EventArgs) _
                              Handles Button1.Click
        FolderBrowserDialog1.SelectedPath = m_path
        If (FolderBrowserDialog1.ShowDialog() = _
            Windows.Forms.DialogResult.OK) Then
            If Not m_path = FolderBrowserDialog1.SelectedPath Then
                m_path = FolderBrowserDialog1.SelectedPath
                ComboBox1.Items.Clear()
                For Each filename As String In _
                    System.IO.Directory.GetFiles(m_path)
                    ComboBox1.Items.Add(filename)
                Next
            End If
        End If
    End Sub
    Private Sub ComboBox1_SelectedIndexChanged(_
        ByVal sender As System.Object, ByVal e As System.EventArgs) _
        Handles ComboBox1.SelectedIndexChanged
        Dim x As WpfInteropCtrl.UserControl1 = _
            CType(ElementHost1.Child, WpfInteropCtrl.UserControl1)
        x.Image = ComboBox1.SelectedItem.ToString
    End Sub
End Class
```

来自 Form1 的代码片段

最后，前面的代码包含 SelectedIndexChanged 事件处理程序，当用户从可用图像文件列表中选择新项时会调用该处理程序。此事件处理程序会检索所选图像路径。
