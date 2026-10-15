
```vb
Private Sub ThisDocument_BeforeSave(ByVal sender As Object, _
    ByVal e As Microsoft.Office.Tools.Word.SaveEventArgs) _
    Handles Me.BeforeSave

Dim res As DialogResult = MessageBox.Show(_
    "Should I save?", "Before Save", _
    MessageBoxButtons.YesNo)

If res = DialogResult.No Then
    ' This code could call a backend data store and then
    ' not save the associated document so the document would remain
    ' unchanged.
    e.Cancel = True
Else
    ' This code would allow you to encourage the user to
    ' always save a new copy of the document
    e.ShowSaveAsDialog = True
End If
End Sub
```

代码片段来自 `ThisDocument.vb`

前面的代码演示了文档上对 `BeforeSave` 事件的自定义重写。请注意，在声明事件处理程序后，代码会创建一个局部变量来保存对话框结果，然后显示一个消息框询问用户是否应保存。通常你不会在此事件上执行此类操作，但这样能让你看到 `SaveEventArgs` 类的两个属性。

如果用户选择不保存，那么你就有选项不保存数据。或者，你也可以不必向用户提供选择，而是直接添加代码，确保用户同时将数据保存到后端数据存储中。无论你需要调用 Web 服务还是更新数据库，这里都是调用该逻辑的好地方。然后你可以保存到数据库，并决定是否确实要更新底层文档。在某些情况下，你可能会悄悄地将数据保存到数据库并且从不保存文档；这样，下次打开文档时，你可以在启动过程中从数据库检索数据。如果你不信任文件系统的只读权限，或者希望确保来自多个不同用户的数据在每次打开文档时都能正确刷新，这是一个特别有用的技巧。

另外，你也可以强制用户执行“另存为”而不是常规保存。这使用了不言自明的 `ShowSaveAsDialog` 属性。其思路同样是，你可能不希望用户替换原始文档；为了防止这种情况，你可以让 Word 自动提示用户以不同名称保存文档。在此过程中你也可以将数据保存到数据库或其他数据存储中。

### 添加功能区（Ribbon）和操作窗格（Actions Pane）

前面的工作为你的应用程序提供了一些基础代码，但它既没有提供自定义功能区，也没有提供自定义任务窗格。因此，在测试之前，让我们先向项目中各添加一个这样的项。要添加这些控件中的任意一个，请在“解决方案资源管理器”中右键单击你的项目，然后选择“添加”按钮以打开“添加新项”对话框。

如图 25-13 所示，当此对话框打开时，你可以从多个类别中选择一项。为了管理可用选项，请选择“Office”类别。这将把可用选项数量从几十个减少到适用于 Word 文档项目的三个。首先添加一个新的功能区栏。有两个选项：XML 和可视化设计器。选择可视化设计器，并为你的控件输入名称 `DocRibbon`。

![](img/d99870e80390742f93963da7be0b2e61_860_0.png)

## 图 25-13

图 25-13 显示了功能区控件的两个备选方案，以保持向后兼容性。以前，如果你要在 Visual Studio 2005 和 VSTO 2005 SE 下为 Office 2007 自定义功能区栏，你无法使用功能区栏的可视化设计器。相反，你需要创建并编辑一个 XML 文件，该文件将定义你的功能区及其上放置的控件。当时既没有设计器，也没有为这项任务定制的工具。

随着 Visual Studio 2008 的发布，VSTO 团队有机会为功能区栏创建可视化设计器。因此，除非你在处理旧版 XML 定义文件，否则应始终选择具有可视化设计支持的功能区。将新控件名称修改为 `DocRibbon` 后，选择“确定”返回 Visual Studio。控件模板将生成控件并打开设计视图。

在设计模式下，请注意，如果你打开控件工具箱，顶部会有一个新的控件类别。左侧的 Office 功能区控件（如图 25-14 所示）提供了可添加到默认功能区的控件列表。请注意，这些控件是 Windows 窗体控件，而不是 WPF 控件。

![](img/d99870e80390742f93963da7be0b2e61_860_1.png)

## 图 25-14

在设计器中向默认的 `Group1` 添加一个按钮。添加按钮后，转到其属性并将按钮的标签改为“隐藏/显示操作窗格”。你也可以选择为按钮添加图标。为此，我进入 Visual Studio 目录，取回了 Visual Studio 2010 附带的一个图标。如果你导航到安装 Visual Studio 10 的文件夹，并浏览文件夹树 `Common7\VS2010ImageLibrary\1033`，你会在此文件夹中找到压缩文件：`VS2010ImageLibrary.zip`。此压缩文件中有数千张不同的图像和图标，可以在你的应用程序中使用。图 25-14 显示了更新后的按钮显示，其中包含一个左侧图标。名为 `NewDocument.bmp` 的图标取自 `VS2010ImageLibrary`。

现在，暂时跳过为此按钮实现处理程序，因为你希望看到功能区和操作窗格的默认行为。相反，右键单击你的项目，再次请求添加新项。在“添加新项”对话框中，选择操作窗格并将其命名为 `DocActionPane`。创建新的操作窗格后，你将再次回到 Visual Studio，这次是在新窗格的设计器中。

与功能区控件不同，操作窗格的设计器不需要特殊的控件集，并且默认具有白色背景。遗憾的是，我在白色背景下区分控件边缘时遇到了麻烦。因此，在做任何其他事情之前，我首先转到控件的属性并选择 `BackColor` 属性。Visual Studio 2010 会打开一个小窗口，其中有“自定义”、“Web”和“系统”三个选项卡，如图 25-15 所示。

![](img/d99870e80390742f93963da7be0b2e61_861_0.png)

图 25-15

这说明了背景的默认设置，这是系统为控件表面定义的颜色。具体来说，“系统”选项卡中的颜色是根据你设置的个人视觉偏好而为你系统定义的。另外两个选项卡则呈现开发人员已选择的颜色选项。如果你只想在设计布局时更改显示颜色，那么最好先记下原始颜色，然后转到突出显示的“自定义”选项卡，选择一种明快的颜色（如红色）来实际高亮显示操作窗格的表面区域。

现在是为这个面板添加一个简单控件的时候了。再次将一个按钮拖到设计界面上。将其放置在左上角，并将标签更改为“Load”（加载）。最终这个按钮将用于将一些数据加载到文档中，但现在是使用 `F5` 测试运行项目的好时机。你的项目将启动，Visual Studio 将启动 Microsoft Word。当 Word 打开时，你的文档将显示你嵌入的图像，如图 25-16 所示。

![](img/d99870e80390742f93963da7be0b2e61_861_1.png)

图 25-16

图 25-16 显示了 Word 中你的自定义文档。此时请留意运行中的应用程序的几点情况。首先，“加载项”（Add-Ins）选项卡被设置为显示自定义功能区栏。这不是错误；即使你创建的是自定义 VSTO 文档解决方案，你对功能区栏所做的自定义也会被自动放入此部分。

接下来，图 25-16 还捕获了之前添加到 `BeforeSave` 事件中的消息框。由于选中了标题栏左上角的“保存”按钮，该事件被触发。在消息框下方，你可以看到添加到文档本身的自定义智能图形。到目前为止一切正常，但文档的操作窗格在哪里？

与功能区栏不同，当你在项目中添加功能区栏时，它会自动与自定义文档关联，而文档操作窗格需要手动与文档关联。因此，图 25-16 中没有显示你的自定义操作窗格，所以下一步就是将操作窗格添加到文档中，并且在本例中根据功能区栏上切换按钮的选择来显示或隐藏它。关闭正在运行的文档，并在调试器停止后返回 Visual Studio。

### 激活操作窗格

如果你选择查看项目中的所有文件，可以选择并打开 `DocActionPane.Designer.vb` 源文件。在此文件中你会发现，你的 `DocActionPane` 类继承自 `System.Windows.Forms.UserControl`。没错，文档操作窗格只是一个自定义的用户控件。

了解这一点就说明，你实际上不仅可以包含单个控件，还可以包含面板控件（如选项卡面板）或显示区域中的其他自定义用户控件。更重要的是，你可以将当前应用程序逻辑中可能正在使用的用户控件直接用于文档操作窗格，而无需做重大更改。不过，为了回答你可能想问的问题，操作窗格没有显示的原因是，Word 和 Excel 都期望你将用户控件与文档的 `ActionsPane` 属性关联起来。

由于操作窗格实际上可用于你项目中的任何用户控件，因此需要由你告诉 Word 分配哪个控件。在 `ThisDocument.vb` 文件中查看文档的代码。前面你已经看到，模板默认创建了 `Startup`（启动）事件处理程序。在此处理程序中添加以下行：

```vb
Private Sub ThisDocument_Startup() Handles Me.Startup

    ActionsPane.Controls.Add(New DocActionPane())

End Sub
```

代码片段来自 `ThisDocument.vb`

这行代码获取与文档关联的内置操作窗格，并向该窗格添加一个控件。当然，你也可以直接将按钮和文本框等项目添加到文档的操作窗格中。但是，正如你所添加的控件所展示的那样，首选方法是创建自定义用户控件，然后将该控件添加到文档中的嵌入式操作窗格中。`New DocActionPane()` 实际上创建了用户控件的一个新实例，并将其放置在操作窗格上。

然而，这不太灵活，因为你希望用户能够显示或隐藏该窗格。与其依赖内置的控件来显示或隐藏窗格，不如让用户可以切换操作窗格的显示状态，这正是你已在功能区中添加按钮的原因。这意味着需要自定义切换按钮的 `Click` 处理程序。在离开 `ThisDocument.vb` 视图之前，请确保关闭此文件的编辑器，以便稍后你能够访问文档本身。

接下来，选择 `DocRibbon`，双击你的按钮，为 `ToggleButton1` 控件的 `Click` 事件添加事件处理程序。这是你希望更改操作窗格显示状态的位置。从功能区栏访问操作窗格的方法是通过应用程序的 `Globals` 集合。在 VSTO 中，你会在该集合中找到对当前文档或工作簿的引用。从这里，你可以访问诸如操作窗格之类的对象。实际上，你可以输入 `Globals.ThisDocument.ActionsPane` 来访问你分配了用户控件的操作窗格。

然而，虽然这确实让你可以访问用户控件，但该控件在你的显示中是由一个框架托管的，因此即使你添加代码来设置文档的 `ActionsPane` 属性的 `Visibility` 属性，它可能也不会产生期望的效果。设置控件的可见性状态只会隐藏控件；它不会隐藏现在空的托管该控件的框架。然而，请记住你可以直接访问操作窗格，因为可能存在你想要做的不只是隐藏和显示操作窗格的情况。例如，如果你想要传递数据或在你的用户控件上设置自定义属性，那么你将利用此对象并从 `Controls` 集合中检索你的控件。

对于此任务，你想要隐藏整个 Document Actions 框架，而不仅仅是它包含的控件。诀窍在于 Word 将该框架视为 `CommandBar`。因此，你需要访问 `CommandBars` 集合。然而，`CommandBars` 集合中有多个不同的控件，因此你需要从此集合中检索 Document Actions 窗格。最可靠的方法是通过名称进行检索，因此你的 `Click` 事件处理程序代码应类似于以下内容：

```vb
Private Sub ToggleButton1_Click(ByVal sender As System.Object, _
    ByVal e As Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs) _
    Handles ToggleButton1.Click
    If ToggleButton1.Checked = True Then
        Globals.ThisDocument.CommandBars("Document Actions").Visible = _
            True
        ToggleButton1.Label = "Hide Action Pane"
    Else
        Globals.ThisDocument.CommandBars("Document Actions").Visible = _
            False
        ToggleButton1.Label = "Show Action Pane"
    End If
End Sub
```

来自 `DocRibbon.vb` 的代码片段

上述代码在你的功能区上的切换按钮被单击时调用。它首先确定切换按钮是被选中还是未选中。`Checked` 属性提供了此信息；如果按钮正在被选中，则下一步是确保 Document Actions 命令栏可见。接下来，代码更新按钮上的文本标签为“Hide Action Pane”。这为用户提供了关于如果再次单击该按钮会发生什么的初始反馈。

同样，代码执行相反操作，隐藏命令栏并更新切换按钮上的文本，以指示用户应再次按下按钮以恢复命令栏。

现在只剩下另一件事要做。默认情况下，因为你将控件分配给操作窗格，你的窗格应被显示。然而，它可能不会显示；用户可能会加载一个抑制 Document Actions 命令栏的加载项。此外，你的切换按钮默认未被选中，而这通常与命令栏被隐藏的状态相关联。

为了解决这些问题，你可以重写功能区的 `Load` 事件。在 `Load` 事件中，检查命令栏的可见性状态并为切换按钮的显示文本和选中状态设置适当的值：

```vb
Private Sub DocRibbon_Load(ByVal sender As System.Object, _
    ByVal e As RibbonUIEventArgs) _
    Handles MyBase.Load
    If Globals.ThisDocument.CommandBars("Document Actions").Visible Then
        ToggleButton1.Checked = True
        ToggleButton1.Label = "Hide Action Pane"
    Else
        ToggleButton1.Label = "Show Action Pane"
    End If
End Sub
```

来自 `DocRibbon.vb` 的代码片段

现在你已经为功能区创建了适当的处理器，可以显示和隐藏操作窗格，这是一个再次测试你的应用程序的好时机。图 25-17 显示了你的自定义文档。它显示了 Add-Ins 功能区，你的 Show/Hide 切换按钮被选中，标题为“Hide Action Pane”。这正确地反映了下一次切换该按钮时，操作窗格的显示将被隐藏。虽然你在书中看不到，但请注意切换按钮如何通过应用 Office 配色方案来指示其视觉状态，以表示一个被选中的控件。在处理自定义 Office 应用程序时，通常会说你的 UI 对熟悉 Office 行为的用户来说会更直观；此示例证明了这一点。

![](img/d99870e80390742f93963da7be0b2e61_864_0.png)

### FIGURE 25-17

图 25-17 显示的另一项内容是实际的 Document Actions 窗口，其中包含你的操作窗格。你可能还记得我将 `DocActionPane` 控件的背景颜色更改为红色。这应该会让你有点担心为什么那个红色背景（在图 25-17 中不明显）仅接近窗口顶部。这是一个只有部分解决方案的挑战。

不幸的是，.NET 控件在 Document Actions 主机中的布局是有限的。你可以请求你的控件填充显示，但此值会被忽略。你可以请求它拉伸，但此设置决定控件的大小是否应默认匹配其内容的显示区域。根本没有一种很好的方法来自动调整自定义显示区域的大小。

你可以返回 Visual Studio 并增加背景的高度。事实上，你可以使背景足够高和足够宽以适应几乎任何大小的显示区域，但真正的挑战与你放置在显示中的控件有关。不幸的是，你不能确定当用户调整 Word 大小时，你选择放置在操作窗格上的关键控件是否始终会被显示。然而，现在此控件上只有一个按钮并且它什么也不做，所以是时候添加一些将数据放置到 Word 文档中的逻辑了。

### Updating a Content Control

到目前为止，放置在你的 Word 文档中的唯一内容是一个简单的图形。虽然这表明你确实可以自定义此 VSTO 文档的内容，但它并没有真正展示动态更新文档内容的能力。第一步是查看 Office 2007 的新功能之一——内容控件。返回你的 Word 文档的设计视图，如图 25-18 所示，并注意工具箱。在此工具箱中有一个标题为 Word Controls 的部分，已被展开。

![](img/d99870e80390742f93963da7be0b2e61_865_0.png)

**FIGURE 25-18**

工具箱此部分中显示的控件是你可应用于文档的控件。让我们看几个简单的示例。添加一些与图 25-18 中所示类似的文本（实际内容并不重要）。然后，在文档中的新行中，添加文本 **Document Name:** 后跟一个或两个制表符。将 `PlainTextContentControl` 拖到你的文档上。在下一行，添加标签 **Application Name:** 后跟一个制表符。然后将 `RichTextContentControl` 拖到文档上。这两个控件将提供一个处理内容控件的简单示例。
