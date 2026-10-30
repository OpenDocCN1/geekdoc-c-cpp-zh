

# 图 1.26

从列表中下拉以向 StatusStrip 添加控件。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_47_0.png)

## 显示日期和时间

你使用 DateTime 结构的属性和方法来检索和格式化当前日期和时间。Now 属性以可用于计算的数字格式保存系统日期和时间。你可以使用以下方法之一来格式化日期和/或时间以供显示：ToShortDateString、ToLongDateString、ToShortTimeString 或 ToLongTimeString。每个方法的实际显示格式取决于本地系统设置。

你可以在任何过程中设置 StatusStripLabels 的显示值；但是，显示不会自动更新。通常，你将在 Form_Load 事件过程中设置初始值，并使用 Timer 组件来更新时间。

## 使用 Timer 组件

要使用 Timer 组件，你将组件添加到窗体，设置一些属性，并在 Timer 的 Tick 事件处理程序中编写代码。从工具箱的 Components 部分添加 Timer 组件。然后在 Properties 窗口中，将 Enabled 属性设置为 true 并设置 Interval 属性。Interval 以毫秒为单位测量；将 Interval 设置为 1000 可使 Timer 的 Tick 事件每秒触发一次。

```
Private Sub Timer1_Tick(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles Timer1.Tick
    ' Update the time in the status bar.

    DateToolStripStatusLabel.Text = Today.ToShortDateString
    TimeToolStripStatusLabel.Text = Now.ToLongTimeString
End Sub
```

## 创建 MDI 项目

你可以使任何窗体成为父窗体。事实上，一个窗体可以同时是父窗体和子窗体（正如一个人可以同时是父母和子女一样）。要将窗体设为父窗体，只需在设计器的 Properties 窗口中将其 `IsMdiContainer` 属性更改为 `true`。在一个项目中，你可以有多个子窗体和多个父窗体。

创建子窗体几乎一样简单。当然，你的项目必须包含不止一个窗体。你在运行时通过代码将窗体设为子窗口。在向父窗体显示子窗体之前，将子窗体的 `MdiParent` 属性设置为当前（父）窗体。

```
Private Sub DisplayChildTwoMenuItem_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles DisplayChildTwoMenuItem.Click
    Display Child Two form.

    Dim AChildTwoForm As New ChildTwoForm
    AChildTwoForm.MdiParent = Me
    AChildTwoForm.Show()
End Sub
```

我们的示例应用程序允许用户显示多个子窗口。因此，每个子窗口的标题栏应该是唯一的。我们可以通过在显示窗体之前在标题栏附加一个数字来实现。这很像 Microsoft Word，其文档为 Document 1、Document 2 等等。

```
' Module-level declarations
Private ChildTwoCounter As Integer

Private Sub DisplayChildTwoMenuItem_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles DisplayChildTwoMenuItem.Click
    ' Display Child Two form.

    Dim AChildTwoForm As New ChildTwoForm
    ChildTwoCounter += 1
    With AChildTwoForm
        .MdiParent = Me
        .Text = "Child Two Document " & ChildTwoCounter.ToString()
        .Show()
    End With
End Sub
```

## 添加 Window 菜单

父窗体应具有 *Window* 菜单（图 1.28）。*Window* 菜单列出打开的子窗口并允许用户在窗口之间切换。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_49_0.png)

> **图 1.28**
> 
> *MDI 应用程序中的 Window 菜单列出打开的子窗口并允许用户选择窗口的排列方式。*

并排列多个子窗口。看看 Word 或 Excel 等应用程序中的 *Window* 菜单。你会看到打开文档的列表以及排列窗口的选项。通常，两个组之间会用分隔条分隔。

要将菜单项指定为 Window 菜单，选择 MenuStrip 组件。在 Properties 窗口中，将 MDIWindowListItem 属性设置为所需的菜单项；通常是 WindowToolStripMenuItem（图 1.29）。

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_50_0.png)

![](img/e2635c7dd07a6ad20d386d5f4f3c5310_50_1.png)

从 MenuStrip 的 MDIWindowListItem 属性下拉列表中选择要作为 Window 菜单的菜单项。

## 布局选项

当打开多个子窗口时，窗口可以按几种不同的布局排列：垂直平铺、水平平铺或层叠。你通过使用 *LayoutMdi* 方法的参数以代码设置布局类型。

```
Me.LayoutMdi(MdiLayout.TileHorizontal)
```

你可以使用三个常量之一：TileHorizontal、TileVertical 和 Cascade。

```
Private Sub TileVerticalToolStripMenuItem_Click(ByVal sender _
    As System.Object, ByVal e As System.EventArgs) _
    Handles TileVerticalToolStripMenuItem.Click
        ' Display open windows tiled vertically.

        Me.LayoutMdi(MdiLayout.TileVertical)
End Sub

Private Sub TileHorizontalToolStripMenuItem_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles TileHorizontalToolStripMenuItem.Click
        ' Display open windows tiled horizontally.

        Me.LayoutMdi(MdiLayout.TileHorizontal)
End Sub

Private Sub CascadeToolStripMenuItem_Click(ByVal sender As Object, _
    ByVal e As System.EventArgs) Handles CascadeToolStripMenuItem.Click
        ' Cascade open windows.

        Me.LayoutMdi(MdiLayout.Cascade)
End Sub
```

## 单例设计模式

在某些应用程序中，例如文字处理器，你可能允许用户打开同一类型的多个子窗口。在其他应用程序中，你只想允许特定类型的一个子窗口。例如，如果你的应用程序有一个 Summary 窗口，用户可以通过选择菜单项来显示它，他或她可能会多次选择该选项。如果你只想允许一个窗体的单个实例，你需要编写代码来实现这一点。

尽管有几种技术可以防止类的多个实例，OOP 推荐的技术是称为单例模式的设计模式。

你可能在想，“什么是设计模式？”基本上，它是解决特定问题的设计逻辑。我们不必每次需要解决一个问题时都重新发明轮子。经验丰富的程序员已经开发并发布了其他程序员可以使用的设计模式和实践。有时我们称之为增加你的程序员“技巧包”。

你可以在 www.codeguru.com/columns/VB/article.php/c6563/ 上找到一篇关于设计模式和单例设计模式的好文章。

要创建单例模式，你在子窗体中定义一个属性，该属性返回类的实例。声明一个共享私有变量来保存类的实例。第一次实例化对象时，实例被分配给变量；在那之前，变量为“Is Nothing”。

*注意：* 如果你不熟悉创建新属性，请参阅第 2 章中的“Creating Properties in a Class”。

```
‘Project:        Ch01MDIApplication
‘Programmer:     EmilyMillsapaugh
‘Date:           June 2009
‘Form:           ChildOneForm
‘Description:    Demonstrates the singleton design pattern to allow only one
                instance of the form.

Public Class ChildOneForm

    Private Shared AnInstance As ChildOneForm

    Public Shared ReadOnly Property Instance() As ChildOneForm
        Get
            If AnInstance Is Nothing Then
                AnInstance = New ChildOneForm
            End If
            Return AnInstance
        End Get
    End Property
End Class
```

单例类还必须在窗体的 Form-Closing 事件处理程序中释放实例。

```
Private Sub ChildOneForm_FormClosing(ByVal sender as Object, ByVal e As System.Windows.Forms.FormClosingEventArgs) Handles Me.FormClosing
' Delete the object when the form is closed.

AnInstance = Nothing
End Sub
```

当你想显示作为单例创建的窗体时，你引用窗体的 Instance 属性而不是使用 New 关键字。

```
Dim AChildOneForm As ChildOneForm = ChildOneForm.Instance()
```

要显示窗体，请在 Focus 方法之前使用 Show 方法。

```
Private Sub ChildOneToolStripMenuItem_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles ChildOneToolStripMenuItem.Click, ChildOneToolStripButton.Click, ChildOneToolStripMenuItem1.Click
' Create an instance of Child One.

Dim AChildOneForm As ChildOneForm = ChildOneForm.Instance()
With AChildOneForm
.MdiParent = Me
.Show()
.Focus()
End With
End Sub
```

在学生光盘上的 Ch01MDIApplication 项目中，ChildOneForm 遵循单例模式，但 ChildTwoForm 不遵循。注意你可以创建 ChildTwoForm 的多个副本，但只能有一个 ChildOneForm。

## 反馈 1.4

编写语句以将 AboutForm 显示为子窗体。

## 闪屏窗体

程序加载时通常会显示一个初始屏幕。此初始窗体称为闪屏。专业应用程序使用闪屏告诉用户程序正在加载和启动。它可以使大型应用程序看起来加载和运行更快，因为在应用程序其余部分加载时屏幕上会出现一些内容。即使我们的程序相对较小且加载速度很快，闪屏也会增添专业感。你可以设置窗体属性并向标准 Windows 窗体添加图像和标签，或使用 Splash Screen 模板。

## 创建你自己的闪屏

