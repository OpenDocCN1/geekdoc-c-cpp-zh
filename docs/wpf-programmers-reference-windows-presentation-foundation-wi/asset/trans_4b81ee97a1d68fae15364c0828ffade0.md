

[content]

程序可以使用控件的 `Password` 属性来查看控件中存储了什么密码。以下代码显示了 `UsePassword` 程序是如何显示你输入的用户名和密码的：

```
// 显示输入的用户名和密码。
private void btnOK_Click(object sender, EventArgs e)
{
    MessageBox.Show(UserName.Text + " 's password is " + pwdPassword.Password);
}
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_170_0.png)

## PasswordBox

除了 `Password` 之外，控件最实用的属性是 `PasswordBox`。此属性决定了用户输入的字符。通常使用默认值（在图 7-11 中产生圆点）是可以的，但如果你不喜欢它，可以将 `PasswordChar` 设置为简单的字符，例如问号（`?`），或者你可以将一个字符复制并粘贴到 XAML 模型中。

你还可以将 `PasswordChar` 设置为数字 HTML 代码。例如，以下代码创建了一个使用字符 `#67`（节符号 `§`）作为密码字符的 `PasswordBox`：

```
<PasswordBox Password="Secret" PasswordChar=&#167;/>
```

## RADIOBUTTON（单选按钮）

`RadioButton` 控件允许用户从一组斥列表中选择一个。如果用户选择了某个 `RadioButton`，同一容器中的所有 `RadioButton` 都会自动取消选择。

（相比之下，一组中的任意数量 `CheckBox` 可以同时被选中。如果用户需要一次选择多个选项，请使用 `CheckBox` 而不是 `RadioButton`）

通常将相关的控件放置在一个组（Group）中很有帮助，这样用户就可以很容易看到它们是相关的。`UseRadioButton` 示例程序如图 7-12 所示，显示了排列在三个 `GroupBox` 中的按钮。如果用户点击了一个 `RadioButton`，该组中的其他按钮将取消选择。

| | 饮食计划 | 停车 |
|---|---|---|
| | Blathery Hall | Full Dining | Close-in |
| | Chelsea Assn | Double City | Campus |
| | Pheldaux | Leftover Lover | Same ZIP Code |

图 7-12

如果你不使用 `GroupBox` 来包围相关的 `RadioButton`，请将它们放置在 `StackPanel`、`Grid` 或其他不显示边界的控件中。

## RELIABLE RADIOBUTTONS（可靠的单选按钮）

如果不使用 `GroupBox` 来分组相关的 `RadioButton`，那么你应该使用其他方法让用户判断哪些按钮是一组的。例如，你可能将不同的 `RadioButton` 组放在行或列中。

`RadioButton` 的属性与 `CheckBox` 非常相似。（在底层，它们是密切相关的控件。）

`IsChecked` 属性决定控件是否被选中。如果控件的 `IsThreeState` 属性为 `True`，`IsChecked` 可以为 `True`、`False` 或 `null`，表示控件处于已选中、未选中或不确定状态（既未选中也非未选中）。

> 困惑的状态
> 三态 `RadioButton` 比三态 `CheckBox` 更让用户感到困惑。从视觉上看，选中状态和不确定状态之间的区别非常小。为了避免混淆，你可能最好不要使用三态 `RadioButton`。请参阅本章前面的“不确定困惑”提示以获得关于不确定状态的更多讨论。

`RadioButton` 最实用的两个事件是 `Checked` 和 `Unchecked`，它们分别在用户选择或取消选择控件时触发。`Click` 事件在用户选择和取消选择控件时都会触发。

## REPEATBUTTON（重复按钮）

`RepeatButton` 控件允许用户在鼠标按在控件上时反复触发 `Click` 事件。通过触发这些事件，用户可以非常快速地多次调用程序执行某项操作。

`RepeatButton` 对程序来说像使用 `Button` 控件一样简单。它简单地捕获控件的 `Click` 事件并采取适当的操作。只要鼠标按住控件，控件就会自动处理触发事件的细节。

`Delay` 属性决定了在开始触发事件之前等待的时间。`Interval` 属性决定了后续触发事件的间隔。默认情况下，`Delay` 和 `Interval` 分别为 500 毫秒和 33 毫秒。

图 7-13 所示的 `UseRepeatButton` 示例显示了按住按钮时触发的情况。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_170_0.png)

## INCONSISTENT INTERVALS（不一致的间隔）

如果不使用 `GroupBox` 来分组相关的 `RadioButton`，那么你应该使用其他方法让用户判断哪些按钮是一组的。例如，你可能将不同的 `RadioButton` 组放在行或列中。

## RICHTEXTBOX（富文本框）

`RichTextBox` 控件允许用户输入带有格式的文本，如字体、颜色、段落、悬挂缩进、项目列表等。`RichTextBox` 是一个非常复杂的控件，包含许多属性和方法，让你控制其行为和内容的格式。`RichTextBox` 自动提供了让用户格式文本的功能。例如，如果用户在控件中选择某些文本并按下 `Ctrl+B`，`RichTextBox` 会将选中文加粗。

`EditingCommands` 也通过代码提供了这些编辑命令。使用 C# 代码可以切换 `RichTextBox` 中的选择是否为编号列表：

```csharp
// 切换编号状态。
private void mParaNumber_Click(object sender, EventArgs e)
{
    EditingCommands.ToggleNumbering.Execute(null, rchBody);
}
```

与其在后台代码中执行编辑命令，你可以在 XAML 代码中指明按钮或菜单项执行它。例如，以下 XAML 代码中的 `Command` 属性使得菜单项在被选中时执行 `AlignLeft` 命令：

```xml
<MenuItem Name="mnuParaAlignLeft" Header="_Left"
Command="EditingCommands.AlignLeft"/>
```

下表列出了最常用的编辑命令以及用户可以按它们调用的键。命令名称是 `EditingCommands` 类中调用该命令的方法名称。

| 命令名称 | 快捷键 |
|---|---|
| AlignCenter | [Ctrl]+E |
| AlignJustify | [Ctrl]+J |
| AlignLeft | [Ctrl]+L |
| AlignRight | [Ctrl]+R |
| DecreaseFontSize | [Ctrl]+OemOpenBracket |
| DecreaseIndentation | [Ctrl]+[Shift]+T |
| EnterLineBreak | [Shift]+[Enter] |
| EnterParagraphBreak | [Enter] |
| IncreaseFontSize | [Ctrl]+OemCloseBracket |
| IncreaseIndentation | [Ctrl]+T |
| ToggleBold | [Ctrl]+B |
| ToggleBullets | [Ctrl]+[Shift]+L |
| ToggleItalic | [Ctrl]+I |

## UseRichTextBox

第 21 章将更多关于文档的内容。`RichTextBox` 是一个非常复杂的控件，包含许多属性和方法，让你控制其行为和内容的格式。以下章节介绍了 `RichTextBox` 控件最实用的功能。

