

| 方法 | 用途 |
|---|---|
| SaveFile | 将控件的文本保存到文件中，支持 RTF 或纯文本等多种格式之一。 |
| SelectAll | 通过将 SelectionStart = 0 并将 SelectionLength 设为文本长度，选中控件的所有文本。 |
| Undo | 撤销最近一次更改。 |

以下代码展示程序如何使用 LoadFile 方法：

```
contentRichTextBox.LoadFile("Test.rtf", RichTextBoxStreamType.RichText);
```

传入 LoadFile 的第一个参数给出文件名，可以是相对于程序当前目录的路径，也可以是完整路径。

第二个参数给出文件类型。RichTextBoxStreamType 枚举列出了可用的文件类型。可用于加载文件的选项有 PlainText、RichText 和 UnicodePlainText。

## 输入提示

当你输入 contentRichTextBox.LoadFile( 时，IntelliSense 会出现并显示如图 7-4 所示的弹出窗口，以展示 LoadFile 方法所需的参数。（由于语句尚未完成，Visual Studio 会添加红色波浪下划线。在我完成输入该语句之前，Visual Studio 会将其标记为错误。）

![](img/d5be6ade75773ca6cec5c78f96a98bb1_146_0.png)

图 7-4

你可以从该方法的三个不同重载版本中选择，每个版本接受不同的参数。方法的重载版本具有相同的名称，但接受不同的参数。你可以使用上下方向键在该方法的可用版本之间滚动。

当你输入参数时，IntelliSense 会更新以描述它期望的下一个参数。图 7-5 显示了在我为第一个参数输入文件名后的 LoadFile 方法。IntelliSense 显示下一个参数应该是名为 fileType 的 RichTextBoxStreamType 类型的值。IntelliSense 甚至在底部显示该值含义的简短说明（尽管信息量不是特别大）。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_146_1.png)

图 7-5

你可以输入 RichTextBoxStreamType 后跟一个点来查看可用选项列表，但还有一种更简单（换句话说，更好）的方法：按 Ctrl+Space。这会让 IntelliSense 显示你可能想要输入的内容列表。此时，IntelliSense 足够智能，能猜到你想输入 RichTextBoxStreamType，因此它会初始选中该类型，甚至显示关于它的更多信息，如图 7-6 所示。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_147_0.png)

图 7-6

现在你可以按 Tab 让 IntelliSense 为你填入高亮的值 RichTextBoxStreamType。

接下来，按 "." 键查看图 7-7 所示的选项列表，选择一个，然后按 Tab 将其添加到代码中。最后，在该行末尾添加一个分号，就完成了。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_147_1.png)

图 7-7

我知道这听起来很麻烦，但稍加练习后，它就会变得出奇地快速和简单。手动输入所有内容时，我大约需要 30 秒才能输入前面的 LoadFile 语句。在 IntelliSense 的帮助下，我可以在 10 秒内输入同一行代码。

以下代码展示程序如何使用 SaveFile 方法。与 LoadFile 一样，第一个参数给出文件名，第二个参数给出文件类型：

```
contentRichTextBox.SaveFile("Test.rtf", RichTextBoxStreamType.RichText);
```

## 使用 WPF 命令

程序可以使用命令来操作 RichTextBox 的内容。该控件还提供用户可以通过交互方式调用的命令。例如，用户可以按 Ctrl+E 使段落居中。

表 7-4 总结了最有用的命令。该控件的 Windows Forms 版本和 WPF 版本所用的命令略有不同。

### 表 7-4

| 操作 | Windows Forms | WPF |
|---|---|---|
| 居中对齐 | Ctrl+E | Ctrl+E |
| 两端对齐 |  | Ctrl+J |
| 左对齐 | Ctrl+L | Ctrl+L |
| 右对齐 | Ctrl+R | Ctrl+R |
| 项目符号 | * | Ctrl+Shift+L |
| 复制 | Ctrl+C | Ctrl+C |
| 剪切 | Ctrl+X | Ctrl+X |
| 减小字号 |  | Ctrl+[ |
| 删除 | Delete | Delete |
| 删除下一个单词 | Ctrl+Delete | Ctrl+Delete |
| 删除上一个单词 | Ctrl+Backspace | Ctrl+Backspace |
| 增大字号 |  | Ctrl+] |
| 编号 | * | Ctrl+Shift+N |
| 粘贴 | Ctrl+V | Ctrl+V |
| 下标 ** | Ctrl++ | Ctrl++ |
| 上标 ** | Ctrl+Shift++ | Ctrl+Shift++ |
| 切换粗体 |  | Ctrl+B |
| 切换插入模式 | Insert | Insert |
| 切换斜体 |  | Ctrl+I |
| 切换下划线 | Ctrl+U | Ctrl+U |

* 在 Windows Forms 中，Ctrl+Shift+L 会循环切换可用的项目符号和编号样式。** 下标和上标的按键组合有点令人困惑。对于下标，按住 Ctrl 键并按 +。对于上标，按住 Ctrl 和 Shift 键并按 +。在 WPF 中，这些命令仅适用于带有下标和上标变体的 OpenType 字体。可以试试 Palatino Linotype 字体。有关 OpenType 字体的更多信息，请参见 msdn.microsoft.com/library/ms745109.aspx。

这两种控件都提供额外的导航命令。例如，Ctrl+右方向键向右移动一个单词，Ctrl+下方向键向下移动一个段落。

WPF 控件还提供一个上下文菜单，其中包含“复制”“剪切”和“粘贴”命令。

有关 WPF 控件命令（包括导航命令）的更多信息，请参见 msdn.microsoft.com/library/system.windows.documents.editingcommands.aspx。

## 试一试

在本“试一试”中，你将为 SimpleEdit 程序的某些菜单项和工具栏按钮添加功能。你将使用 RichTextBox 的属性和方法来实现“编辑”菜单中的命令：撤销、重做、复制、剪切、粘贴、删除和全选。（这也会让相应的按钮无需额外操作即可生效。）

### 本课要求

在本课中，你将：

- 复制你在第 6 课练习 9 中构建的 SimpleEdit 程序。
- 将程序的 TextBox 替换为名为 `contentRichTextBox` 的 RichTextBox。
- 添加代码以处理“编辑”菜单的命令。
  - 添加撤销代码。
  - 添加重做代码。
  - 添加复制代码。
  - 添加剪切代码。
  - 添加粘贴代码。
  - 添加删除代码。
  - 添加全选代码。

> 注意 你可以从网站 www.wrox.com/go/csharp24hourtrainer2e 下载本课的代码和资源。

### 提示

- 对于“删除”菜单项，只需将控件的 `SelectedText` 属性设置为空字符串：""。

### 分步操作

- 复制你在第 6 课练习 9 中构建的 SimpleEdit 程序（或从本书网站下载第 6 课的版本）。
- 将程序的 `TextBox` 替换为名为 `contentRichTextBox` 的 `RichTextBox`。
- 添加代码以处理“编辑”菜单的命令。

1. 在窗体设计器中打开程序的窗体。单击 `MenuStrip`，展开“编辑”菜单，然后双击“撤销”菜单项。
2. 将占位调用 `MessageBox.Show` 替换为以下代码行，使事件处理程序如下所示：
3. 对其他“编辑”菜单项重复前两个步骤。以下代码展示了新的事件处理程序：

```
private void editUndoMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.Undo();
}
```

```
private void editUndoMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.Undo();
}

private void editRedoMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.Redo();
}

private void editCopyMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.Copy();
}

private void editCutMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.Cut();
}

private void editPasteMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.Paste();
}

private void editDeleteMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.SelectedText = "";
}

private void editSelectAllMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.SelectAll();
}
```

完成后，测试程序的新功能。RichTextBox 更引人注目的功能之一是能够从剪贴板粘贴不同类型的项目。例如，将图片复制到剪贴板，然后使用该程序将其粘贴到 RichTextBox 中。

