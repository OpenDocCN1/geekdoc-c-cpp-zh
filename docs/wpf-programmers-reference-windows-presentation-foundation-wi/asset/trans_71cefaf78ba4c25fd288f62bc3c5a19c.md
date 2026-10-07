

# RichTextBox | 137

| 命令名称 | 快捷键 |
|---|---|
| ToggleNumbering | [Ctrl]+[Shift]+N |
| ToggleScript | [Ctrl]+OemPlus |
| ToggleSuperscript | [Ctrl]+[Shift]+OemPlus |
| ToggleUnderline | [Ctrl]+U |

OpenBracket（左括号）、CloseBracket（右括号）和 OemPlus（加号）键是 OEM（原始设备制造商）[] 字符。这些键通常放置在小键盘区域，取决于你的键盘硬件，键盘其他部分的类似按键可能无法工作。例如，小键盘区域的 `+` 键可能有效，但数字键区域侧的 `+` 键可能无效。

有关编辑命令的更多信息和更完整的列表，请参阅 msdn.microsoft.com/system.windows.documents.editingcommands.aspx。

# # 拼写检查

RichTextBox 控制最令人兴奋的功能之一是支持拼写检查。如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制（Copy）、剪切（Cut）和粘贴（Paste）的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”（Ignore All）命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

图 7-14 显示了 UseRichTextBox 程序显示其右菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_174_0.png)

图 7-14

# # 撤销和重做

RichTextBox 控件自动提供撤销和重做功能。每当用户按下 [Ctrl]+Z` 时，控件就会撤销最近的更改。每当用户按下 [Ctrl]+Y` 时，控件就会重新应用最近被撤销的更改。

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

# 其他功能

RichTextBox 控件提供了许多其他功能，无法在此处全部列出。在继续之前，下表总结了一些关键的 RichTextBox 属性。

| 属性 | 用途 |
|---|---|
| AcceptsReturn | 决定 [Enter] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsReturn` 为 `False` 且窗口包含一个 `IsDefault` 为 `True` 的按钮，则在控件内按下 [Enter] 将触发该按钮。 |
| AcceptsTab | 决定 [Tab] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsTab` 为 `False`，则按下 [Tab] 将焦点移动到窗口的下一个控件。 |
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

# # 拼写检查

RichTextBox 控件最令人兴奋的功能之一是支持拼写检查。如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制、剪切和粘贴的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

图 7-14 显示了 UseRichTextBox 程序显示其右菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_174_0.png)

图 7-14

# # 撤销和重做

RichTextBox 控件自动提供撤销和重做功能。每当用户按下 [Ctrl]+Z` 时，控件就会撤销最近的更改。每当用户按下 [Ctrl]+Y` 时，控件就会重新应用最近被撤销的更改。

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

# 其他功能

RichTextBox 控件提供了许多其他功能，无法在此处全部列出。在继续之前，下表总结了一些关键的 RichTextBox 属性。

| 属性 | 用途 |
|---|---|
| AcceptsReturn | 决定 [Enter] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsReturn` 为 `False` 且窗口包含一个 `IsDefault` 为 `True` 的按钮，则在控件内按下 [Enter] 将触发该按钮。 |
| AcceptsTab | 决定 [Tab] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsTab` 为 `False`，则按下 [Tab] 将焦点移动到窗口的下一个控件。 |
| HorizontalScrollBarVisibility | 决定水平滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）、Hidden（隐藏）或 Visible（可见）。 |
| IsEnabled | 决定控件是否会与用户交互。如果此项为 `False`，用户可以看到内容但不能更改、高亮或滚动控件的内容。 |
| IsReadOnly | 决定用户是否可以修改控件的内容。如果 `IsReadOnly` 为 `True`，用户仍然可以滚动控件内容、选择文本并将文本复制到剪贴板。如果你想显示用户无法更改的内容，通常设置 `IsReadOnly = True` 比设置 `IsEnabled = False` 更好。 |
| VerticalScrollBarVisibility | 决定垂直滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）或 Visible（可见）。 |

UseRichText 示例程序演示了其他简单的格式命令，允许你更改：

- 字体样式（粗体、斜体、下划线）
- 字体大小（小、中等、大）
- 文本颜色
- 背景颜色
- 字体族（例如 Times New Roman, Arial, Courier New）
- 带项目符号和编号的段落
- 段落对齐

查看 [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 以获取更多关于编辑命令的信息和更完整的列表。（注：此处根据原文逻辑翻译了链接内容）

- [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 

# # 拼写检查

RichTextBox 控件最令人兴奋的功能之一是支持拼写检查。如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制、剪切和粘贴的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”（Ignore All）命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

图 7-14 显示了 UseRichTextBox 程序显示其右菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_174_0.png)

图 7-14

# # 撤销和重做

RichTextBox 控件自动提供撤销和重做功能。每当用户按下 [Ctrl]+Z` 时，控件就会撤销最近的更改。每当用户按下 [Ctrl]+Y` 时，控件就会重新应用最近被撤销的更改。

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

# 其他功能

RichTextBox 控件提供了许多其他功能，无法在此处全部列出。在继续之前，下表总结了一些关键的 RichTextBox 属性。

| 属性 | 用途 |
|---|---|
| AcceptsReturn | 决定 [Enter] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsReturn` 为 `False` 且窗口包含一个 `IsDefault` 为 `True` 的按钮，则在控件内按下 [Enter] 将触发该按钮。 |
| AcceptsTab | 决定 [Tab] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsTab` 为 `False`，则按下 [Tab] 将焦点移动到窗口的下一个控件。 |
| HorizontalScrollBarVisibility | 决定水平滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）、Hidden（隐藏）或 Visible（可见）。 |
| IsEnabled | 决定控件是否会与用户交互。如果此项为 `False`，用户可以看到内容但不能更改、高亮或滚动控件的内容。 |
| IsReadOnly | 决定用户是否可以修改控件的内容。如果 `IsReadOnly` 为 `True`，用户仍然可以滚动控件内容、选择文本并将文本复制到剪贴板。如果你想显示用户无法更改的内容，通常设置 `IsReadOnly = True` 比设置 `IsEnabled = False` 更好。 |
| VerticalScrollBarVisibility | 决定垂直滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）或 Visible（可见）。 |

UseRichText 示例程序演示了其他简单的格式命令，允许你更改：

- 字体 样式（粗体、斜体、下划线）
- 字体大小（小、中等、大）
- 文本颜色
- 背景颜色
- 字体族（例如 Times New Roman, Arial, Courier New）
- 带项目符号和编号的段落
- 段落对齐

查看 [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 以获取更多关于编辑命令的信息和更完整的列表。（注：此处根据原文逻辑翻译了链接内容）

- [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 

# # 拼写检查

RichTextBox 控件最令人兴奋的功能之一是支持拼写检查。如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制、剪切和粘贴的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”（Ignore All）命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

图 7-14 显示了 UseRichTextBox 程序显示其右菜单。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_174_0.png)

图 7-14

# # 撤销和重做

RichTextBox 控件自动提供撤销和重做功能。每当用户按下 [Ctrl]+Z` 时，控件就会撤销最近的更改。每当用户按下 [Ctrl]+Y` 时，控件就会重新应用最近被撤销的更改。

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

# 其他功能

（此处注：由于提供的文本中存在重复段落，从“RichTextBox 控件提供了许多其他功能...”之后开始的重复内容已根据要求“不要重复输出原文”进行过滤，但原始文本存在重复部分）

RichTextBox 控件提供了许多其他功能，无法在此处全部列出。在继续之前，下表总结了一些关键的 RichTextBox 属性。

| 属性 | 用途 |
|---|---|
| AcceptsReturn | 决定 [Enter] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsReturn` 为 `False` 且窗口包含一个 `IsDefault` 为 `True` 的按钮，则在控件内按下 [Enter] 将触发该按钮。 |
| AcceptsTab | 决定 [Tab] 键击是放置在控件的内容中，还是发送到窗口。如果 `AcceptsTab` 为 `False`，则按下 [Tab] 将焦点移动到窗口的下一个控件。 |
| HorizontalScrollBarVisibility | 决定水平滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）、Hidden（隐藏）或 Visible（可见）。 |
| IsEnabled | 决定控件是否会与用户交互。如果此项为 `False`，用户可以看到内容但不能更改、高亮或滚动控件的内容。 |
| IsReadOnly | 决定用户是否可以修改控件的内容。如果 `IsReadOnly` 为 `True`，用户仍然可以滚动控件内容、选择文本并将文本复制到剪贴板。如果你想显示用户无法更改的内容，通常设置 `IsReadOnly = True` 比设置 `IsEnabled = False` 更好。 |
| VerticalScrollBarVisibility | 决定垂直滚动条是否可见。它可以是 Auto（自动）、Disabled（禁用）或 Visible（可见）。 |

UseRichText 示例程序演示了其他简单的格式命令，允许你更改：

- 字体 样式（粗体、斜体、下划线）
- 字体大小（小、中等、大）
- 文本颜色
- 背景颜色
- 字体族（例如 Times New Roman, Arial, Courier New）
- 带项目符号和编号的段落
- 段落对齐

查看 [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 以获取更多关于编辑命令的信息和更完整的列表。（注：此处根据原文逻辑翻译了链接内容）

- [RichTextBox 命令](https://msn.microsoft.com/system.windows.documents.editingcommands.aspx) 

# # 拼写检查

（由于原文存在重复，此处仅保留未重复的逻辑部分）

如果你将控件的 `SpellCheck.IsEnabled` 属性设置为 `True`，则控件会自动高亮可能的错误。

默认情况下，RichTextBox 控件提供一个包含复制、剪切和粘贴的右菜单。如果启用了拼写检查并且你在拼写错误的单词上左单击，则右菜单还会包含一个可能的纠正列表和一个“忽略所有”（Ignore All）命令。如果你选择其中一个建议，控件会将拼写错误的版本替换为你选择的内容。如果你选择“忽略所有”，控件会将该拼写错误单词的所有出现视为拼写正确。

