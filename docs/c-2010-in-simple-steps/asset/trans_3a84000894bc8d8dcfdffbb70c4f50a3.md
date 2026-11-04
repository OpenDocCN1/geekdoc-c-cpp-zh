
表 6.20 列出了 SaveFileDialog 类的注目属性：

**表 6.20：SaveFileDialog 类的注目属性**

| 属性 | 说明 |
|---|---|
| `CreatePrompt` | 获取或设置一个值，该值指示如果指定了不存在的文件，另存为对话框是否提示用户创建新文件 |
| `OverwritePrompt` | 获取或设置一个值，指定如果用户指定了已存在的文件名，另存为对话框是否显示警告 |

表 6.21 列出了 SaveFileDialog 类的注目方法：

**表 6.21：SaveFileDialog 类的注目方法**

| 方法 | 说明 |
|---|---|
| `OpenFile` | 以读写权限打开所选文件 |
| `Reset` | 将所有对话框选项重置为默认值 |

让我们创建一个名为 SaveFileDialogDemo 的简单 Windows 窗体应用程序来使用另存为对话框。执行以下步骤进行创建：

- 1. *重复* 本章 Using the ToolStrip Control 标题下的步骤 1-4。
- 2. 在新建项目对话框的 Name 文本框中输入 *SaveFileDialogDemo* 作为应用程序的名称。在 Location 下拉组合框中输入要保存应用程序的文件夹路径。
- 3. 在新建项目对话框中单击 OK 按钮。SaveFileDialogDemo 应用程序已创建。
- 4. 在设计器中选择 Form1 表单并按 F4 键打开属性窗口，并将 Form1 表单的 Text 属性设置为 SaveFileDialogDemo。
- 5. 从工具箱拖动 Label、Button 和 TextBox 控件并将其放置在 Form1 表单上，并将它们的属性设置为表 6.22 中给出的值。

**表 6.22：Form1 上标签、按钮和文本框的属性值**

| 控件 | 属性 | 值 |
|---|---|---|
| `label1` | Text | 输入文件内容如下： |
|  | Location | 12, 18 |
| `button1` | Text | 保存 |
|  | Location | 107, 223 |
|  | Size | 75, 23 |
| `textBox1` | Multiline | True |
|  | Location | 15, 56 |
|  | Size | 257, 134 |

- 6. 从工具箱的 Dialogs 选项卡拖放 SaveFileDialog 控件到 Form1，如图 C-6.39 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_213_0.png)

图 C-6.39

- 7. 双击 Save 按钮并在其 Click 事件中添加第 6.9 节中给出的突出显示的代码：

**清单 6.9：显示 button1_Click 事件的代码**

```csharp
private void button1_Click(object sender, EventArgs e)
{
    saveFileDialog1.Filter = "Text Files (*.txt)|*.txt*";
    saveFileDialog1.InitialDirectory = Environment.SpecialFolder.MyDocuments.ToString();
    if (saveFileDialog1.ShowDialog() == DialogResult.OK)
    {
        if (saveFileDialog1.CheckFileExists == false)
            System.IO.File.WriteAllText(saveFileDialog1.FileName, textBox1.Text,
                System.Text.Encoding.UTF8);
    }
    textBox1.Text = "";
}
```

在清单 6.9 中，saveFileDialog1 控件的 Filter 属性被设置为仅在另存为对话框中显示文本文件。此外，saveFileDialog1 控件的 InitialDirectory 属性被设置为位于 C 盘上的 MyDocuments 文件夹。这意味着保存文件的初始位置是 MyDocuments 文件夹。如果用户在另存为对话框中单击 OK 按钮，则会检查计算机上是否存在与用户指定的名称相同的文件。如果不存在此类文件，则使用 System.IO.File.WriteAllText() 方法将用户在 textBox1 控件中输入的文本保存到指定的文件中。

> 注
> Filter 和 InitialDirectory 属性在 FileDialog 类中定义，SaveFileDialog 类继承了该类。

- 8. 按 F5 键运行应用程序。
- 9. 在 Enter the file contents below 标签下方的文本框中输入一些文本（图 C-6.40）。在后续步骤中，您在文本框中输入的文本将使用另存为对话框保存到文件中。
- 10. 如图 C-6.40 所示单击 Save 按钮：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_214_0.png)

图 6.40

另存为对话框出现。
- 11. 在另存为对话框顶部的位置下拉组合框中指定文件的适当位置。
- 12. 在文件名文本框中输入要保存文件的名称。在此，我们已将文件名输入为 MyFile。请注意，必须连同文件名一起指定扩展名。
- 13. 在对话框中单击 Save 按钮以保存文件。

现在，让我们学习打印控件。

## 使用打印控件

在 C# 2010 中，有多个控件允许您在 .NET 应用程序中集成打印文档的 UI 功能。C# 2010 中与打印过程相关的两个主要控件如下：

- PrintDocument control
- PrintDialog control

现在，让我们在下一节中学习这两个控件。

### PrintDocument 控件

PrintDocument 控件表示一个对象，其中包含用户想要打印的文档。此控件允许您设置各种属性，例如 DefaultPageSettings 和 DocumentName 以打印文档。由于 PrintDocument 控件没有 UI，因此在运行时不可见。

PrintDocument 控件是存在于 System.Drawing.Printing 命名空间中的 PrintDocument 类的实例。PrintDocument 类具有多个属性和方法，可促进打印过程。

表 6.23 列出了 PrintDocument 类的注目属性：

**表 6.23：PrintDocument 类的注目属性**

| 属性 | 说明 |
|---|---|
| DefaultPageSettings | 获取或设置要打印的所有页面的默认页面设置 |
| DocumentName | 获取或设置打印文档时要显示的文档名称 |
| PrinterSettings | 获取或设置打印文档的打印机 |

表 6.24 列出了 PrintDocument 类的注目事件：

**表 6.24：PrintDocument 类的注目事件**

| 事件 | 说明 |
|---|---|
| BeginPrint | 在调用 Print() 方法后但在打印第一页之前发生 |
| EndPrint | 在打印文档的最后一页后发生 |
| PrintPage | 当需要为当前页输出打印内容时发生 |
| QueryPageSettings | 在 PrintPage 事件发生前立即发生 |

PrintDocument 类还具有名为 Print 的方法，该方法允许您启动文档的打印过程。

### PrintDialog 控件

PrintDialog 控件显示打印对话框，允许您打印文档。打印对话框允许您选择打印机并指定各种选项和设置，例如是否打印所有页面或仅特定页面以及要打印的文档副本数。请注意，没有 PrintDialog 控件；文档将使用默认打印机和打印机设置打印。

PrintDialog 控件是存在于 System.Windows.Forms 命名空间中的 PrintDialog 类的实例。PrintDialog 类提供了多个属性和方法，可用于打印文档。

表 6.25 列出了 PrintDialog 类的注目属性：

**表 6.25：PrintDialog 类的注目属性**

| 属性 | 说明 |
|---|---|
| AllowCurrentPage | 获取或设置一个值，该值指示用户是否具有仅打印当前页面的功能 |
| AllowPrintToFile | 获取或设置一个值，该值指示“打印到文件”复选框是否启用 |
| AllowSomePages | 获取或设置一个值，该值指示用户是否具有指定页范围的功能 |
| Document | 获取或设置 PrintDocument 对象 |
| PrinterSettings | 获取或设置在打印对话框中修改的打印机设置 |
| PrintToFile | 获取或设置一个值，该值指示“打印到文件”复选框是否被选中 |

PrintDialog 类提供了一个名为 Reset 的方法，允许您将所有对话框选项重置为默认值。

在使用 PrintDialog 控件显示打印对话框之前，您必须将其 Document 属性设置为 PrintDocument 对象。此外，您还需要将 PrintDocument 对象的 PrinterSettings 属性设置为 PrintDialog 控件的 PrinterSettings 属性。

让我们创建一个名为 PrintingDemo 的 Windows 窗体应用程序来演示 PrintDocument 和 PrintDialog 控件的使用。执行以下步骤创建 PrintingDemo 应用程序：

- 1. 重复本科章 Using the ToolStrip Control 部分下的步骤 1-4。
- 2. 在新建项目对话框的 Name 文本框中输入 PrintingDemo 作为应用程序的名称。在 Location 下拉组合框中输入要保存应用程序的文件夹路径。现在，单击 OK 按钮。PrintingDemo 应用程序已创建。
- 3. 在设计器中选择 Form1 表单并按 F4 键打开属性窗口。将 Form1 表单的 Text 属性设置为 PrintingDemo。
- 4. 从工具箱拖动 Label、Button 和 TextBox 控件并将其放置在设计器中的 Form1 表单上。将这些控件的属性设置为表 6.26 中给出的值：

**表 6.26：标签、按钮和文本框控件的属性值**

| 控件 | 属性 | 值 |
|---|---|---|
| `label1` | Text | 输入要打印的文本： |
| `label1` | Location | 25, 31 |
| `button1` | Text | 打印 |
| `button1` | Location | 101, 206 |

