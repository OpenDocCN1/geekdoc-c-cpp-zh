

如果在你的项目菜单下没有出现“属性”菜单项，请打开“解决方案资源管理器”（Ctrl+Alt+L），选中项目名称（它会以粗体字体显示），然后重试。

“启动窗体”下拉列表将包含应用程序中可用的窗体。 在此下拉列表中选择一个窗体，该窗体将在应用程序启动时成为首先显示的窗体。

你也可以使用此对话框来指定其他启动任务，例如显示启动画面。 要控制这些附加选项，必须选中标记为“启用应用程序框架”的复选框。

## 通过 Sub Main 显示窗体

如果你不想使用加载 Windows 窗体应用程序的默认方式，可以在代码中显式控制启动过程。 例如，你可能出于需要在第一个窗体加载前运行身份验证逻辑而这样做。

要控制启动过程，首先在代码模块中创建一个名为 Sub Main 的空子程序。 如果你的项目中尚未包含代码模块，可能需要创建一个。 代码模块在第 2 章中有讨论。

在项目属性对话框中取消选中标记为“启用应用程序框架”的复选框。 “启动窗体”下拉列表的标签将更改为“启动对象”，并且它将包含一个新条目：Sub Main。

最后，创建 Sub Main 的逻辑。 典型的逻辑如下所示：

```
Sub Main()
' Do start up work here
Dim f As New Form1
Application.Run(f)
End Sub
```

请注意，当你创建 Sub Main 逻辑时，不要使用先前的技术通过 Show 方法显示窗体。 窗体的对象引用会立即超出作用域。 窗体将短暂出现，然后应用程序将终止。 相反，在 Sub Main 中，你的逻辑应使用 Application 对象的 Run 方法来加载起始窗体。

## 有关 Application 类的更多信息

Application 类包含许多共享方法和属性，可用于管理你的 Windows 窗体应用程序。 除了前面显示的 Run 方法之外，Application 类还有一个 Exit 方法来结束应用程序，以及一个 Restart 方法来使应用程序关闭并立即重新启动。

Application 类还具有用于管理应用程序的有用事件。 例如，ApplicationExit 事件在应用程序即将关闭时触发。

## 窗体的启动位置

通常，你希望窗体首次出现时居中显示在屏幕上。 当你设置 StartPosition 属性时，VB.NET 会自动为你完成此操作。 表 14-1 显示了设置及其含义。

TABLE 14-1: Options for Starting Position of a Form

| STARTPOSITION VALUE | EFFECT |
|---|---|
| Manual | Shows the form positioned at the values defined by the form's Location property |
| CenterScreen | Shows the form centered on the screen |
| WindowsDefaultLocation | Shows the form at the window's default location |
| WindowsDefaultBounds | Shows the form at the window's default location, with the window's default bounding size |
| CenterParent | Shows the form centered in its owner |

## 窗体边框

窗体在 Windows 窗体中有许多边框选项。 FormBorderStyle 属性用于设置边框选项，并且选项会影响用户可以如何操作窗体。 FormBorderStyle 可用的选项包括以下内容：

- None — No border, and the user cannot resize the form
- FixedSingle — Single 3-D border, and the user cannot resize the form
- Fixed3D — 3-D border, and the user cannot resize the form
- FixedDialog — Dialog-box-style border, and the user cannot resize the form
- Sizeable — Same as FixedSingle, except that the user can resize the form
- FixedToolWindow — Single border, and the user cannot resize the form
- SizeableToolWindow — Single border, and the user can resize the form

每个选项对窗体标题栏中出现的按钮都有不同的影响。 有关详细信息，请查看 FormBorderStyle 属性的帮助主题。

## 始终置顶 — TopMost 属性

某些窗体需要始终保持可见，即使它们没有焦点，例如浮动工具栏和教程窗口。 在 Windows 窗体中，窗体有一个名为 TopMost 的属性。 将其设置为 True 可使窗体覆盖其他窗体，即使它没有焦点。

请注意，TopMost 设置为 True 的窗体位于所有应用程序之上，而不仅仅是托管应用程序。 如果你需要窗体仅位于应用程序中其他窗体之上，则此功能由所有者窗体提供。

## 所有者窗体

与 TopMost 属性一样，所有者窗体浮动在应用程序之上，但它不会干扰使用应用程序。 一个例子是查找和替换框。 然而，所有者窗体并不位于所有窗体之上，而只是位于其所有者窗体之上。

当一个窗体由另一个窗体拥有时，它会随所有者窗体一起最小化和关闭。 所有者窗体永远不会在其所有者窗体后面显示，但它们不会阻止其所有者窗体获得焦点并被使用。 然而，如果你想单击被所有者窗体覆盖的区域，则必须先将所有者窗体移开。

一个窗体一次只能有一个“所有者”。 如果一个已经由 Form1 拥有的窗体被添加到 Form2 的所有者窗体集合中，则该窗体不再由 Form1 拥有。

有两种方法可以使一个窗体由另一个窗体拥有。 可以在所有者窗体中完成，也可以在被拥有窗体中完成。

## AddOwnedForm 方法

在所有者窗体中，另一个窗体可以通过 AddOwnedForm 方法变为拥有。 以下代码使 Form2 的实例成为 Form1 的拥有窗体。 此代码将位于 Form1 中的某处，通常放置在显示 Form2 实例到屏幕的行之前：

```
Dim frm As New Form2
Me.AddOwnedForm(frm)
```

## Owner 属性

关系也可以在被拥有窗体中设置。 这是通过窗体的 Owner 属性完成的。 这里有一个方法，可以在 Form2 内部工作，使其由作为函数参数传递的窗体拥有：

```
Public Sub MakeMeOwned(frmOwner As Form)
    Me.Owner = frmOwner
End Sub
```

由于此技术需要在被拥有窗体内部引用所有者，因此它不像在所有者窗体中使用 AddOwnedForm 方法那样常用。

## OwnedForms 集合

所有者窗体可以通过 OwnedForms 属性访问其拥有的窗体集合。 这里是遍历窗体拥有的窗体的代码：

```
Dim frmOwnedForm As Form
For Each frmOwnedForm In Me.OwnedForms
    Console.WriteLine(frmOwnedForm.Text)
Next
```

Code snippet from StartForm

所有者窗体可以通过 RemoveOwnedForm 属性删除一个被拥有的窗体。 这可以在与前一个示例类似的循环中完成，代码如下：

```
Dim frmOwnedForm As Form
For Each frmOwnedForm In Me.OwnedForms
    Console.WriteLine(frmOwnedForm.Text)
    Me.RemoveOwnedForm(frmOwnedForm)
Next
```

Code snippet from StartForm

此循环将导致所有者窗体停止拥有其所有从属窗体。 请注意，这些“解除从属”窗体不会被卸载，它们只是不再被拥有。

## 使窗体透明和半透明

Windows 窗体提供高级功能来使窗体半透明，或使窗体的部分透明。 你甚至可以更改窗体的整个形状。

## Opacity 属性

Opacity 属性衡量窗体是不透明还是透明。 0% 的值使窗体完全透明。 100% 的值使窗体完全可见。 任何大于 0 且小于 100 的值都会使窗体部分可见，就像幽灵一样。 请注意，0% 的不透明度值会禁用单击窗体的功能。

非常低的不透明度级别，范围在 1 或 2%，会使窗体实际上不可见，但仍允许窗体被单击。 这意味着 Opacity 属性有可能创建恶作剧应用程序，这些应用程序位于其他应用程序前面并“窃取”它们的鼠标单击和其他事件。

> 在“属性”窗口中使用百分比值来设置不透明度，但在代码中设置 Opacity 属性时，必须使用 0 到 1 之间的值，其中 0 等同于 0%，1 等同于 100%。

不应完全遮挡其背景的工具和对话框窗口是使用 Opacity 的一个示例。 通过逐渐淡出应用程序的用户界面来设置“免费试用”的到期时间是另一个示例。

