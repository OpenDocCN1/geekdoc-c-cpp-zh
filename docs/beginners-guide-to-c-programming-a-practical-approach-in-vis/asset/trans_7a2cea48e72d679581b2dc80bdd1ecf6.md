

```csharp
private void changeColourToolStripMenuItem_Click(object sender, EventArgs e)
{
    this.BackColor = Color.White;
}

private void exitToolStripMenuItem_Click(object sender, EventArgs e)
{
    Application.Exit();
}
```

代码 6.2

- **7.** 现在我们可以生成并运行项目。程序将显示如下：

![](img/41d82527c4e41cdb7e56259564306ddc_137_0.png)

图 6.3. 包含 MenuStrip 的程序

- **8.** 我们可以使用 **Alt+F** 组合键打开文件菜单，或像平常一样使用鼠标。当我们选择**更改颜色**项时，窗体的背景色将变为白色，如图 6.4 所示。同样，如果我们选择**退出**项，应用程序将退出。

![](img/41d82527c4e41cdb7e56259564306ddc_137_1.png)

图 6.4. 通过菜单项更改背景色

### 6.1.2. ContextMenuStrip

ContextMenuStrip 用于提供右键菜单。它可以添加到窗体本身或控件上。其属性与 MenuStrip 的属性类似。

让我们在一个简单示例中，将 ContextMenuStrip 添加到 RichTextBox 上，实现复制、粘贴和清除功能：

- 1. 在 Visual Studio 中创建一个新的 C# 项目。

- 2. 在窗体上添加一个 RichTextBox 和一个 ContextMenuStrip。与 MenuStrip 一样，ContextMenuStrip 将出现在窗体下方，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_138_0.png)

图 6.5. 添加到窗体上的 ContextMenuStrip

- 3. 如图 6.6 所示，像在 MenuStrip 示例中那样，将**复制**、**粘贴**和**清除**项添加到 ContextMenuStrip。

- 4. 将 RichTextBox 的 Name 设置为 **rClickRichTextBox**。

- 5. 我们需要创建 ContextMenuStrip 项的默认 Click 事件处理程序。为此，像通常一样双击每个项，然后生成代码 6.3 中所示的事件处理方法。

![](img/41d82527c4e41cdb7e56259564306ddc_139_0.png)

图 6.6. 向 ContextMenuStrip 添加项

```csharp
private void copyToolStripMenuItem_Click(object sender, EventArgs e)
{
}

private void pasteToolStripMenuItem_Click(object sender, EventArgs e)
{
}

private void clearToolStripMenuItem_Click(object sender, EventArgs e)
{
}
```

代码 6.3

- 6. 现在，我们将为复制、粘贴和清除功能添加所需的代码行。代码行 `rClickRichTextBox.Copy();` 和 `rClickRichTextBox.Paste();` 分别执行复制和粘贴操作。请注意，这些代码行不会复制和粘贴 RichTextBox 的全部内容，而只会复制和粘贴选中的文本。代码行 `rClickRichTextBox.Clear();` 清除 RichTextBox，正如方法名 `Clear()` 所示。我们将这些代码行插入到事件处理方法中，如下所示：

```csharp
private void copyToolStripMenuItem_Click(object sender,
    EventArgs e)
{
    rClickRichTextBox.Copy();
}

private void pasteToolStripMenuItem_Click(object sender,
    EventArgs e)
{
    rClickRichTextBox.Paste();
}

private void clearToolStripMenuItem_Click(object sender,
    EventArgs e)
{
    rClickRichTextBox.Clear();
}
```

代码 6.4

- 7. 我们创建了 ContextMenuStrip，但没有将它分配给任何窗体控件。为了在 RichTextBox 中使用它，我们必须将 RichTextBox 的 ContextMenuStrip 属性设置为 contextMenuStrip（本例中使用的 ContextMenuStrip 的 Name），如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_140_0.png)

图 6.7. 设置 RichTextBox 的 ContextMenuStrip

- 8. 现在我们可以生成并运行项目。将出现以下程序窗口：

![](img/41d82527c4e41cdb7e56259564306ddc_141_0.png)

图 6.8. 程序窗口

右键菜单没有按预期出现在窗体上。让我们像图 6.8 所示，向 RichTextBox 中输入一些文本。现在，我们可以使用右键菜单的复制、粘贴和清除功能，分别如图 6.9、图 6.10 和图 6.11 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_141_1.png)

图 6.9. 填充了格式化文本的 RichTextBox

![](img/41d82527c4e41cdb7e56259564306ddc_142_0.png)

图 6.10. 通过右键菜单选中并复制了一些文本

![](img/41d82527c4e41cdb7e56259564306ddc_142_1.png)

图 6.11. 使用右键菜单粘贴选中的文本

![](img/41d82527c4e41cdb7e56259564306ddc_142_2.png)

图 6.12. 使用右键菜单项“清除”清空 RichTextBox

### 6.1.3. StatusStrip

StatusStrip 用于向用户提供信息，通常位于窗体的底部。StatusStrip 可以包含各种项类型，例如 StatusLabel、ProgressBar 和 DropDownButton。当我们将 StatusStrip 放置在窗体上时，它会位于其默认位置：窗体底部。

让我们在一个简单示例中利用 StatusStrip：

- 1. 在 Visual Studio 中创建一个新的 C# 项目。

- 2. 在窗体上添加一个 StatusStrip。默认情况下，它将出现在窗体的底部。

- 3. 现在，我们可以通过单击 StatusStrip 的箭头来添加内容，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_143_0.png)

图 6.13. 向 StatusStrip 添加 StatusLabel

- 4. 当我们添加 StatusLabel 时，它会出现在 StatusStrip 上，等待设置：

![](img/41d82527c4e41cdb7e56259564306ddc_143_1.png)

图 6.14. 添加到 StatusStrip 的 StatusStripLabel

- 5. 按如下所示，将 StatusStripLabel 的 Text 属性设置为 **这是一个 StatusStripLabel**：

![](img/41d82527c4e41cdb7e56259564306ddc_144_0.png)

图 6.15. 设置 StatusStripLabel 的 Text 属性

- 6. 现在我们可以生成并运行项目。StatusStrip 及其项 StatusStripLabel 将出现在程序的状态栏中，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_144_1.png)

图 6.16. StatusStrip 及其 StatusStripLabel 出现在窗体底部

![](img/41d82527c4e41cdb7e56259564306ddc_146_0.png)

图 6.18. 添加到 ToolStrip 的各种项

- 5. 将 Label 的 Text 设置为“这是一个 ToolStrip 标签”。

- 6. 向 MenuStrip 添加“文件”项。这仅用于演示目的；我们之前已经学习了如何使用 MenuStrip。

- 7. 生成并运行项目。程序应如下所示，ToolStrip 位于 MenuStrip 控件下方：

![](img/41d82527c4e41cdb7e56259564306ddc_146_1.png)

图 6.19. 示例程序中的 MenuStrip 和 ToolStrip

### 6.1.5. ToolStripContainer

ToolStripContainer 提供一个可以包含多个 ToolStrip 的区域。
让我们在一个示例中使用它：

- 1. 在 Visual Studio 中创建一个 C# 项目。

- 2. 将一个 ToolStripContainer 拖放到窗体上，默认情况下它将浮动，如图 6.20 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_147_0.png)

图 6.20. 将 ToolStripContainer 添加到窗体

- 3. 我们可以将其停靠在窗体上，这意味着它将跨越整个窗体，其中间面板将包含窗体中使用的其他控件。从 Tasks 菜单中选择“在窗体中停靠填充”，即可使其填充窗体；该菜单可通过单击 ToolStripContainer 顶部的箭头打开：

![](img/41d82527c4e41cdb7e56259564306ddc_147_1.png)

图 6.21. 使用 ToolStripContainer 填充窗体

- 4. 现在，我们可以通过单击相应的箭头来打开区域，将 ToolStrip 插入 ToolStripContainer 的顶部、左侧、右侧或底部区域，这些区域将包含 ToolStrip，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_148_0.png)

图 6.22. 在 ToolStripContainer 上打开右侧 ToolStrip 区域

- 5. 现在，我们可以将 ToolStrip 拖放到已打开的区域，并按通常方式使用该 ToolStrip：

![](img/41d82527c4e41cdb7e56259564306ddc_148_1.png)

图 6.23. 将 ToolStrip 添加到已打开的区域

由于可以向 ToolStrip 中的按钮添加图像，因此可以轻松创建具有专业外观的应用程序，这些应用程序在 ToolStripContainer 中拥有用于打开文件、保存文件、剪切、复制、粘贴等功能的图像按钮。

### 6.2. 对话框类型控件

对话框类型控件为用户提供用于进行选择的小型对话框。

### 6.2.1. ColorDialog

ColorDialog 用于选择颜色。它具有以下重要属性：

- **DialogResult**：返回的颜色值的类型。
- **ShowDialog**：用于显示对话框窗口。

让我们在一个示例中使用 ColorDialog 来设置窗体的背景颜色：

- 1. 在 Visual Studio 中创建一个 C# 项目。

- 2. 将一个 ColourDialog 拖放到窗体上。它将出现在窗体下方的窗格中。将其 Name 属性设置为 selectColourDialog。

- 3. 在窗体上添加一个 Button。将 Button 的 Name 和 Text 属性分别设置为 selectColourButton 和“选择背景颜色”。窗体应如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_149_0.png)

图 6.24. 窗体及其控件的当前状态

