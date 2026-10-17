
```
<MenuItem IsCheckable="True" IsChecked="True">
  <MenuItem.Header>
    <StackPanel Orientation="Horizontal">
      <Image Stretch="None" Source="Grayiley.bmp" Margin="0,0,20,0"/>
      <Image.BitmapEffect>
        <DropShadowEffect/>
      </Image.BitmapEffect>
    </Image>
    <Label Content="_Drop Shadow"/>
  </StackPanel>
  </MenuItem.Header>
</MenuItem>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_168_0.png)

# 无限制勾选 (UNLIMITED FREE CHECKING)

WPF 对可勾选项的支持几乎是自动的。如果 `MenuItem` 的 `IsCheckable` 为 `True`，那么当用户点击时，程序会自动选中该项。`MenuItem` 提供了 `Checked` 和 `Unchecked` 事件让程序知道发生了什么。

如果你只需要项，你就完成了。如果你需要菜单项是互斥的（例如，你希望图 7-10 所示的项中只有一个被选中），你需要添加额外的代码，在某一项被选中时取消其他项的选中。

# 随处可见的菜单

普通的菜单横跨应用程序顶部，但并没有阻止你将其放在其他地方。例如，你可以在 `GroupBox` 内部或 `TabControl` 的页中添加菜单，以提供仅适用于这些控件的命令。你甚至可以对菜单应用变换使其旋转或倾斜。

不要让你的用户感到困惑，不要到处都是菜单。如果你让菜单变得太令人混乱，你将花费大量时间向困惑的用户解释。

最后一点值得提一下。你可以设置 `MenuItem` 的 `Icon` 属性来决定当项未被选中时显示的图片。当项被选中时，它会显示一个复选标记，类似于图 7-10 中“Drop Shadow”旁边的那个。

# 密码框 (PASSWORDBOX)

`PasswordBox` 是一种相对简单的文本框，它将用户输入的字符替换为点（•）或屏幕上的其他特殊字符。在内部，控件会跟踪输入的内容，但防止用户看到它。简单来说，它防止了恶作剧的 Phil 从用户肩膀偷窥密码。

图 7-11 所示的 `UsePasswordBox` 示例程序演示了 `PasswordBox`。输入用户名和密码。当你输入密码时，`PasswordBox` 显示一系列点。当你点击 OK 按钮时，程序将显示你输入的用户名和密码。

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
>
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

# RichTextBox | 137

| 命令名称 | 快捷键 |
|---|---|
| ToggleNumbering | [Ctrl]+[Shift]+N |
| ToggleScript | [Ctrl]+OemPlus |
| ToggleSuperscript | [Ctrl]+[Shift]+OemPlus |
| ToggleUnderline | [Ctrl]+U |

OpenBracket（左括号）、CloseBracket（右括号）和 OemPlus（加号）键是 OEM（原始设备制造商）[] 字符。这些键通常放置在小键盘区域，取决于你的键盘硬件，键盘其他部分的类似按键可能无法工作。例如，小键盘区域的 `+` 键可能有效，但数字键区域侧的 `+` 键可能无效。

有关编辑命令的更多信息和更完整的列表，请参阅 `msdn.microsoft.com/system.windows.documents.editingcommands.aspx`。

## 拼写检查

RichTextBox 控制最令人兴奋的功能之一是支持拼写检查。如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制（Copy）、剪切（Cut）和粘贴（Paste）的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”（Ignore All）命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

图 7-14 显示了 UseRichTextBox 程序显示其右菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_174_0.png)

图 7-14

## 撤销和重做

RichTextBox 控件自动提供撤销和重做功能。每当用户按下 `[Ctrl]+Z` 时，控件就会撤销最近的更改。每当用户按下 `[Ctrl]+Y` 时，控件就会重新应用最近被撤销的更改。

控件还提供了你可以通过编程方式管理撤销栈的工具。`CanUndo` 和 `CanRedo` 属性指示控件是否有可以撤销或重做的操作。`Undo` 和 `Redo` 方法调用撤销或重做操作。

RichTextBox 程序的编辑（Edit）菜单包含撤销（Undo）和重做（Redo）命令。当用户打开编辑菜单时，以下代码检查 RichTextBox 控件的 `CanUndo` 和 `CanRedo` 属性，以确定哪些菜单项应该启用。例如，如果用户最近没有撤销过命令，则 `CanUndo` 返回 `False` 且 `mnuEditRedo` 菜单被禁用。

```
// 启用或禁用撤销和重做命令。
private void mnuEditSubmenuOpened(object sender, RoutedEventArgs e)
{
    mnuUndo.IsEnabled = (richTextBox.CanUndo);
    mnuEditRedo.IsEnabled = (richTextBox.CanRedo);
}
```

以下代码显示了程序如何调用控件的 Undo 和 Redo 方法。

```
// Undo.
private void mnuEditUndo_Click(object sender, RoutedEventArgs e)
{
    richTextBox.Undo();
}
```

```
// Redo.
private void mnuEditRedo_Click(object sender, RoutedEventArgs e)
{
    richTextBox.Redo();
}
```

## 其他功能

RichTextBox 控件提供了许多其他功能，无法在此处全部列出。在继续之前，下表总结了一些关键的 RichTextBox 属性。

| 属性 | 用途 |
|---|---|
| AcceptsReturn | 决定 `[Enter]` 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsReturn` 为 `False` 且窗口包含一个 `IsDefault` 为 `True` 的按钮，则在控件内按下 `[Enter]` 将触发该按钮。 |
| AcceptsTab | 决定 `[Tab]` 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsTab` 为 `False`，则按下 `[Tab]` 将焦点移动到窗口的下一个控件。 |
| HorizontalScrollBarVisibility | 决定水平滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）、Hidden（隐藏）或 Visible（可见）。 |
| IsEnabled | 决定控件是否会与用户交互。如果此项为 `False`，用户可以看到内容但不能更改、高亮或滚动控件的内容。 |
| IsReadOnly | 决定用户是否可以修改控件的内容。如果 `IsReadOnly` 为 `True`，用户仍然可以滚动控件内容、选择文本并将文本复制到剪贴板。如果你想显示用户无法更改的内容，通常设置 `IsReadOnly = True` 比设置 `IsEnabled = False` 更好。 |
| VerticalScrollBarVisibility | 决定垂直滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）或 Visible（可见）。 |

UseRichText 示例程序演示了其他简单的格式命令，允许你更改：

字体 字体样式（粗体、斜体、下划线）

- 字体大小（小、中等、大）

- 文本颜色

- 背景颜色

- 字体族（例如 Times New Roman, Arial, Courier New）

- 带项目符号和编号的段落

- 段落对齐

查看 [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 以获取更多关于编辑命令的信息和更完整的列表。（注：此处根据原文逻辑翻译了链接内容）

- [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx)

## 拼写检查

RichTextBox 控件最令人兴奋的功能之一是支持拼写检查。如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制、剪切和粘贴的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

图 7-14 显示了 UseRichTextBox 程序显示其右菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_174_0.png)

图 7-14

## 撤销和重做
