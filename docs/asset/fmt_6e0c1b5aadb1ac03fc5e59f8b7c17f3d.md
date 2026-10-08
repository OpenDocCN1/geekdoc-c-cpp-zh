
`Private Sub multipage_AddControl(ByVal Index Long, ByVal Control AS MSForms.Control)`

在这里，`Index` 是 `Page` 的索引或名称，`Control` 是被添加的控件。例如，`cmdAddControl_Click` 过程添加了三个按钮（`opt1`, `opt2`, `opt3`），`fraOptions` 框现在包含了三个 个控件。

```
Private Sub cmdAddControl_Click()

Dim opt1 As OptionButton

Dim opt2 As OptionButton

Dim opt3 As OptionButton

Set opt1 = fraOptions.Controls.Add("OptionButton", , , "opt1")

opt1.Left = 10

opt1.Top = 10

opt1.Caption = "Option 1"

opt1.AutoSize = True

Set opt2 = fraOptions.Controls.Add("OptionButton", , , "opt2")

opt2.Left = 10

opt2.Top = 30

opt2.Caption = "Option 2"

opt2.AutoSize = True

Set opt3 = fraOptions.Controls.Add("OptionButton", , , "opt3")

opt3.Left = 10

opt3.Top = 50

opt3.Caption = "Option 3"

opt3.AutoSize = True

MsgBox "The frame now contains " & fraOptions.Controls.Count & " controls."

End Sub
```

## RemoveControl 事件

当控件从框架（`Frame`）、多页控件（`MultiPage`）或用户表单（`User Form`）中删除时，无论是运行时程序化还是手动都会触发 `RemoveControl` 事件。（要手动删除控件，用户通常会使用用户表中专门为此目的设计的控件。这里需要进行一些编程——用户无法自行删除控件。）除 `MultiPage` 控件以外的所有控件，`RemoveControl` 事件的语法如下：

```
Private Sub object_RemoveControl(ByVal Control As MsForms.Control)
```

在此，`object` 是一个有效对象，`Control` 是一个有效控件。对于 `Page` 控件，`multipage_RemoveControl` 事件的语法如下：

```
Private Sub multipage_RemoveControl(ByVal Index As Long, ByVal Control As MsForms.Control)
```

在此，`multipage` 是一个有效的 `MultiPage` 对象。对于 `Page` 控件，`Index` 指定 `MultiPage` 控件中包含要删除控件的项。

## 适用于许多或大多数控件的事件

本节讨论了适用于许多或大多数控件的事件。其中某些事件适用于 `UserForm` 对象，例如 `Click`（点击）；`Change`（更改）；`Enter`（进入）和 `Exit`（退出）；`BeforeUpdate`（更新前）和 `AfterUpdate`（更新后）；`KeyDown`（键按下）、`KeyUp`（键释放）和 `KeyPress`（按）；`MouseDown`（鼠标按下）、`MouseUp`（鼠标释放）、`Mouse`（鼠标移动）；`BeforeDragOver`（拖过前）；`BeforeDropPaste`（粘贴前）；`DblClick`（双击）以及 `Error`（错误）。

## Click 事件

`Click` 是 VBA 中常见的事件，适用于 `Check`、`ComboBox`、`CommandButton`、`Frame`、`Image`、`Label`、`ListBox`、`MultiPage`、`OptionButton`、`TabStrip` 和 `ToggleButton` 控件。它不支持 `TextBox`、`ScrollBar` 或 `SpinButton` 控件，但它是 `UserForm` 对象的成员。

当用户用左鼠标键点击控件，或者当用户为具有多个可能值的控件选择值时，就会发生 `Click` 事件。对于大多数控件，用户每点击一次控件，事件就会触发一次。有少数例外：

- 点击禁用的控件会触发用户表单的 `Click` 事件（如果用户是通过该控件点击表单）。
- `OptionButton` 控件的 `Click` 事件在用户点击选项按钮以选择它时触发。如果该选项按钮已被选中，点击它不会产生任何影响。（相反，`CheckBox` 控件的 `Click` 事件在用户每次点击复选框时都会触发——无论是为了选中还是为了清除。）
- `ListBox` 控件的 `Click` 事件在用户点击从列表中选择某项时触发（而不是当用户点击下拉箭头或组合框的下拉部分时触发）。如果用户点击了已选中的项，`Click` 事件将不会再次触发。
- `ToggleButton` 控件的 `Click` 事件发生在每次切换按钮被点击以及其 `Value` 属性发生变化时。这意味着使用 `ToggleButton` 控件的 `Click` 事件来切换其 `Value` 并不是一个好主意。
- 当选中的 `CommandButton` 控件并按下空格键时，触发 `Click` 事件。
- 当用户在没有选择其他命令的情况下按下回车键时，默认命令按钮（`Default` 属性设置为 `True` 的按钮）会触发 `Click` 事件。
- 当用户按下 Esc 键时，`Cancel` 属性设置为 `True` 的命令按钮会触发 `Click` 事件。带有快捷键的控件的 `Click` 事件在用户按下快捷键时也会触发。

对于除 `TabStrip` 和 `MultiPage` 控件以外的所有控件，`Click` 事件不需要参数，如下所示：

```
Private Sub object_Click()
```

对于 `TabStrip` 控件或 `MultiPage` 控件，你的代码必须对 `Index` 参数做出响应，这是一个所需的 `Long`（数据类型）参数，VBA 通过它来标识受影响的控件页或页：

```
Private Sub object_Click(ByVal Index As Long)
```

在此，`object` 是一个有效的 `MultiPage` 控件或 `TabStrip` 控件。

> 事件顺序：用户点击（并再次点击）时发生了什么
事件触发的顺序有时对程序员非常重要。如果你不理解事件发生的顺序，可能会编写出导致事件冲突——甚至相互触发的代码。
当用户点击命令按钮时，如果点击转移到命令按钮，该按钮的 `Enter` 事件会在 `Click` 事件之前发生。命令按钮的 `Enter` 事件触发，这通常会阻止 `Click` 事件触发。
当用户点击控件时，触发的第一个事件是 `MouseDown` 事件，它在用户按下鼠标键时触发。然后，当用户释放鼠标键时触发 `MouseUp` 事件。`Click` 事件发生在 `MouseUp` 事件之后。如果用户在 Windows 的双击间隔时间内进行点击，则会触发 `DClick` 事件，随后是另一个 `MouseUp` 事件。

## Change 事件

`Change` 事件适用于 `CheckBox`、`ComboBox`、`ListBox`、`MultiPage`、`OptionButton`、`ScrollBar`、`SpinButton`、`TextBox` 和 `ToggleButton` 控件。当控件的 `Value` 属性发生时，触发此事件。这种变化可以通过用户的操作（例如在文本框中输入文本、选择选项按钮、选中或清除复选框、点击切换按钮或更改 `MultiPage` 控件上显示的页面）或通过运行时的程序化操作发生。

请记住，当通过用户操作触发 `Change` 事件时，该操作也可能触发 `Click` 事件。（即使发生这种情况，与 `Click` 相比，`Change` 被认为是确定控件新 `Value` 的更好方法——尽管对于许多目的来说，`Click` 也能很好地工作）。在设计时手动更改控件的 `Value` 属性不会触发 `Change` 事件。

`Change` 事件的语法如下：

```
Private Sub object_Change()
```

## ENTER 和 EXIT 事件

`Enter` 和 `Exit` 事件适用于 `CheckBox`、`ComboBox`、`CommandButton`、`Frame`、`ListBox`、`MultiPage`、`OptionButton`、`ScrollBar`、`SpinButton`、`TabStrip`、`TextBox` 和 `ToggleButton` 控件。当用户将从一个控件移动到另一个控件时，触发 `Enter` 和 `Exit` 事件。`Enter` 事件在控件接收焦点时触发，`Exit` 事件在控件失去焦点时触发。

`Enter` 事件的语法为：

```
Private Sub object_Enter()
```

`Exit` 事件的语法为：

```
Private Sub object_Exit(ByVal Cancel AS MSForms.ReturnBoolean)
```

## BEFOREUPDATE 事件

`BeforeUpdate` 事件适用于 `CheckBox`、`ComboBox`、`ListBox`、`OptionButton`、`ScrollBar`、`SpinButton`、`TextBox` 和 `ToggleButton` 控件。这些事件发生在控件中的值发生变化时；你可以使用该事件评估是否执行更新。

`BeforeUpdate` 事件的语法为：

```
Private Sub object_BeforeUpdate(ByVal Cancel As MSForms.ReturnBoolean)
```

在此，`object` 是一个有效对象，`Cancel` 是一个指示事件状态的必需参数。默认设置为 `False` 使控件处理事件；`True` 则阻止更新的执行。

## AFTERUPDATE 事件

`AfterUpdate` 事件适用于 `CheckBox`、`ComboBox`、`ListBox`、`OptionButton`、`ScrollBar`、`SpinButton`、`TextBox` 和 `ToggleButton` 控件。在用户更改控件中的信息且更新已执行后，触发这些事件。

`AfterUpdate` 事件的语法对于其适的所有控件和对象都是相同的：

```
Private Sub object_AfterUpdate()
```

# KEYDOWN 和 KEYUP 事件

`KeyDown` 和 `KeyUp` 事件适用于 `UserForm` 对象的 `CheckBox`、`ComboBox`、`CommandButton`、`Frame`、`ListBox`、`MultiPage`、`OptionButton`、`ScrollBar`、`SpinButton`、`TabStrip`、`Textbox` 和 `Toggle` 控件。这些事件不适用于 `Image`（图像）和 `Label`（标签）控件。

当用户在键盘上按下某个按键时，触发 `KeyDown`。当用户松开按键时，触发 `KeyUp`。当按键发送到用户控件或使用 `SendKeys` 语句程序化发送时，也会发生 `KeyDown` 和 `KeyUp` 事件。当用户表单包含一个 `Default` 属性设置为 `True` 的 `CommandButton` 控件时，按下 Enter 键不会触发这些事件；当用户表单包含一个 `Cancel` 属性设置为 `True` 的 `CommandButton` 控件时，按下 Esc 键也不会触发这些事件。

当鼠标将焦点移动到另一个控件时，原始控件会触发 `KeyDown` 事件，而焦点移动到的控件会触发 `KeyPress` 和 `KeyUp` 事件。

`KeyPress` 在 `KeyDown` 事件之后、`KeyUp` 事件之前触发。
`KeyDown` 事件的语法如下：

```
Private Sub object_KeyDown(ByVal KeyCode As MSForms.ReturnInteger, ByVal Shift As Integer)
```

`KeyUp` 事件的语法如下：

```
Private Sub object_KeyUp(ByVal KeyCode As MSForms.ReturnInteger, ByVal Shift As Integer)
```

此处，`object` 是对象名称，是必需的。`KeyCode` 是一个必需的 `Integer` 类型参数，用于指定所按按键的代码。例如，字母 T 的代码是 84。键码不是 ANSI 值——它是一个识别键盘上按键的特殊数字。

`Shift` 是一个必需的参数，用于指定按了哪个 Shift、Ctrl 或 Alt 键。请使用表 15.7 显示的常量或值。

表 15.7：Shift 常量和值

| CONSTANT | VALUE | DESCRIPTION |
|---|---|---|
| fmShiftMask | 1 | 按下了 Shift 键 |
| fmCtrlMask | 2 | 按下了 Ctrl 键 |
| fmAltMask | 4 | 按下了 Alt 键 |

# KEYPRESS 事件

`KeyPress` 事件是 `CheckBox`、`ComboBox`、`CommandButton`、`Frame`、`ListBox`、`MultiPage`、`OptionButton`、`ScrollBar`、`SpinButton`、`TabStrip`、`Textbox` 和 `Toggle` 控件的成员。它也是 `UserForm` 对象的成员。`Label` 控件没有 `KeyPress` 事件。

当用户在目标控件或对象拥有焦点时，按下可打印字符、Ctrl 加字母、Ctrl 加特殊字符（符号）、Esc 或 Backspace（退格）键时，会触发 `KeyPress` 事件。按下 Tab 键、Enter 键或箭头键不会触发 `KeyPress` 事件，按键也不会将焦点从当前控件移动到另一个控件。

从技术上讲，只有 ANSI 键会触发 `KeyPress` 事件。Delete 键不是 ANSI 键，但在文本框中按 Delete 键删除文本时不会触发 `KeyPress` 事件。但是，使用 Backspace 键删除文本框中的相同文本会触发该事件，因为 Backspace 是 ANSI 键。

`KeyPress` 事件在 `KeyDown` 事件之后、`KeyUp` 事件之前触发。当你使用 `SendKeys` 程序化向用户表单发送按键时，也会触发该事件。`KeyPress` 事件的语法如下：

```
Private Sub object_KeyPress(ByVal KeyAscii As MSForms.ReturnInteger)
```

此处，`object` 是一个必需参数，用于指定有效对象，`KeyAscii` 是一个必需的 `Integer`，用于指定 ANSI 键码。要获取 ANSI 键码，请使用 `Asc` 函数。例如，`Asc("t")` 返回字母 t 的 ANSI 键码（代码为 116）。

默认情况下，`KeyPress` 事件处理所按按键的代码——通俗地说，你按什么就得到什么。例如，如果你按下 l，你就得到一个 l；如果你按下 Delete 键，你就得到一个 Delete 操作；以此此类推。通过使用 `KeyPress` 事件过程，你可以执行诸如检查（例如在用户必须输入数值时过滤掉非数字按键）。

# MouseDown 事件和 MouseUp 事件

`MouseDown` 和 `MouseUp` 事件适用于 `UserForm` 对象的 `CheckBox`、`ComboBox`、`CommandButton`、`Frame`、`Label`、`ListBox`、`MultiPage`、`OptionButton`、`ScrollBar`、`SpinButton`、`TabStrip`、`TextBox` 和 `ToggleButton` 控件。当用户按下按钮时，触发 `MouseDown` 事件，当用户松开该按钮时，发生 `MouseUp` 事件。`MouseDown` 和 `MouseUp` 事件的语法如下：

```
Private Sub object_MouseDown(ByVal Button As Integer, ByVal Shift As Integer, ByVal X As Single, ByVal Y As Single)
```

```
Private Sub object_MouseUp(ByVal Button As Integer, ByVal Shift As Integer, ByVal X As Single, ByVal Y As Single)
```

对于 `MultiPage` 和 `TabStrip` 控件，它增加了一个 `Index` 参数来指定页或标签页的索引。此处，`object` 是一个必需参数，用于指定有效对象。`Button` 是一个必需的 `Integer`，用于指定触发事件的是哪个按钮。表 15.8 列出了 `Button` 的值。

表 15.8：Button 常量

| CONSTANT | VALUE | DESCRIPTION |
|---|---|---|
| fmButtonLeft | 1 | 左键（主） |
| fmButtonRight | 2 | 右键（主） |
| fmButtonMiddle | 4 | 中键 |

`Shift` 是一个必需参数，用于指定按了哪个 Shift、Ctrl 或 Alt 键。表 15.9 列出了 `Shift` 的值。

表 15.9：Shift 值

| VALUE | KEY PRESSED |
|---|---|
| 1 | Shift |
| 2 | Ctrl |
| 3 | Shift+Ctrl |
| 4 | Alt |
| 5 | Alt+Shift |
| 6 | Alt+Ctrl |
| 7 | Alt+Shift+Ctrl |

# MouseMove 事件

`MouseMove` 事件适用于 `UserForm` 对象的 `CheckBox`、`ComboBox`、`CommandButton`、`Frame`、`Label`、`ListBox`、`MultiPage`、`OptionButton`、`ScrollBar`、`SpinButton`、`TabStrip`、`TextBox` 和 `ToggleButton` 控件。当用户将鼠标指针移动到目标控件或对象上方时触发该事件。控件的 `MouseMove` 方法如下：
