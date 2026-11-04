
1. 使用筛选器：

    Text Files|*.txt|RTF Files|*.rtf|All Files|*.*

2. 使用类似以下的代码：

```
private void openFileButton_Click(object sender, EventArgs e)
{
    if (testOpenFileDialog.ShowDialog() == DialogResult.OK)
    {
        openFileTextBox.Text = testOpenFileDialog.FileName;
        testSaveFileDialog.FilterIndex =
            testOpenFileDialog.FilterIndex;
    }
}
```

当用户单击“保存文件”按钮时，显示 SaveFileDialog。使用与 OpenFileDialog 相同的筛选器。如果用户单击“保存”，则使“保存文件”文本框显示对话框的 FileName 属性，并将 OpenFileDialog 的 FilterIndex 设置为等于 SaveFileDialog 的 FilterIndex。

1. 使用筛选器：

    Text Files|*.txt|RTF Files|*.rtf|All Files|*.*

2. 使用类似以下的代码：

```
private void saveFileButton_Click(object sender, EventArgs e)
{
    if (testSaveFileDialog.ShowDialog() == DialogResult.OK)
    {
        saveFileTextBox.Text = testSaveFileDialog.FileName;
        testOpenFileDialog.FilterIndex =
            testSaveFileDialog.FilterIndex;
    }
}
```

当用户单击“打印”按钮时，显示 PrintDialog。忽略返回结果。

1. 使用类似以下的代码：

```
private void printButton_Click(object sender, EventArgs e)
{
    testPrintDialog.ShowDialog();
}
```

当用户单击“打印预览”按钮时，显示 PrintPreviewDialog。忽略返回结果。

1. 使用类似以下的代码：

```
private void printPreviewButton_Click(object sender, EventArgs e)
{
    testPrintPreviewDialog.ShowDialog();
}
```

## 练习

1. [WPF] 使用 WPF 程序重复“试一试”。由于 WPF 程序无法直接使用 ColorDialog 或 FontDialog 中选定的值，只需在文本框中显示用户的选择即可。对于 ColorDialog，显示对话框的 Color.ToString() 值。对于 FontDialog，显示对话框的 Font.ToString() 值。（提示：不必担心设置对话框的 FilterIndex 属性。）

2. [WPF] 复制你在练习 1 中编写的程序并使用颜色信息。使用类似以下的代码设置窗口的背景颜色：

```
Color backColor = new Color()
{
    A = 255,
    R = colorDialog.Color.R,
    G = colorDialog.Color.G,
    B = colorDialog.Color.B
};
Background = new SolidColorBrush(backColor);
```

对于字体颜色，使用类似的技术设置字体文本框的前景色。（为整个窗口设置前景色更困难。）

3. [WPF] 创建一个与图 8-6 所示类似的程序。
提示：
- 如果任何事件处理程序在程序启动时导致程序崩溃，请在事件处理程序开头添加以下语句，以防止程序在控件创建之前尝试使用它们。

```
if (!IsLoaded) return;
```
- 对于字体 RadioButtons 的 Checked 事件，使用类似以下的代码：

```
sampleLabel.FontFamily = new FontFamily("Arial");
```
- 对于 Slider 的 ValueChanged 事件，使用类似以下的代码：

```
if (!IsLoaded) return;
sizeGroupBox.Header = "Size: " + sizeSlider.Value.ToString();
sampleLabel.FontSize = sizeSlider.Value;
```
- 为 Bold CheckBox 提供 Checked 和 Unchecked 事件处理程序。使它们将 sampleLabel.FontWeight 设置为 FontWeights.Bold 或 FontWeights.Normal。
- 为 Normal、Italic 和 Oblique RadioButtons 提供 Checked 事件处理程序。使它们分别将 sampleLabel.FontStyle 设置为 FontStyles.Normal、FontStyles.Italic 和 FontStyles.Oblique。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_169_0.png)

4. [SimpleEdit] 复制你在第 7 课练习 6 中构建的 SimpleEdit 程序（或从书的网站下载第 7 课的版本），并为“文件”菜单的“打开”和“另存为”命令添加文件打开和保存对话框。使用允许用户选择 RTF 文件、文本文件或所有文件的 Filter 属性。继续使用 RichTextBox 的 LoadFile 和 SaveFile 方法，即使它们对非 RTF 文件不起作用。

5. [SimpleEdit] 复制你在练习 4 中构建的 SimpleEdit 程序，并为“格式”菜单的“字体”项和字体工具栏按钮添加字体选择对话框。如果用户选择字体并单击“确定”，则使 RichTextBox 的所选文本使用所选字体。

6. [SimpleEdit] 复制你在练习 5 中构建的 SimpleEdit 程序并修改它，使其允许用户在字体对话框上选择颜色。

7. [SimpleEdit] 复制你在练习 6 中构建的 SimpleEdit 程序，并为“格式”和上下文菜单的“文字颜色”和“背景颜色”项添加颜色选择对话框。（允许自定义颜色。）

注意 请在 www.wrox.com/go/csharp24hourtrainer2evideos 在线选择第 8 课的视频。

## 9

## 创建和显示新窗体

本书迄今为止大部分内容都涉及构建窗体。之前的课程解释了如何在窗体上添加、排列和处理控件的事件。它们解释了如何使用特定类型的控件，例如按钮、MenuStrips、contextMenuStrips 和 toolStrips。使用这些技术，你可以构建一些相当不错的窗体，使用简单的代码来操作属性。然而，到目前为止，你只学会了如何使用单个窗体。

在本课中，你将学习如何在单个程序中显示多个窗体。你将了解如何向项目添加新窗体以及如何显示一个或多个该窗体的实例。一旦掌握了这些技术，你就可以创建显示任意数量窗体的程序，用于各种不同的目的。

### 添加新窗体

要向项目添加新窗体，请打开“项目”菜单并选择“添加 Windows 窗体”，以查看图 9-1 所示的对话框。

保持 Windows 窗体模板被选中，输入新窗体类型的一个好名称，然后单击“添加”。单击“添加”后，Visual Studio 会将新窗体类型添加到项目中。图 9-2 显示了解决方案资源管理器中的新窗体。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_173_0.png)

图 9-1

![](img/d5be6ade75773ca6cec5c78f96a98bb1_173_1.png)

图 9-2

现在你可以向新窗体添加标签、文本框、按钮、菜单栏以及你喜欢的任何其他控件。

> 注意 请记住，要在窗体设计器中打开窗体，请在解决方案资源管理器中双击它。

当你向项目添加新窗体时，你实际上是在添加一种新的窗体类型，而不是该类型的新的实例。如果你向项目添加 MakeUserForm 类型然后运行程序，你仍然只会看到原始的启动窗体（名字很吸引人的 Form1），而 MakeUserForm 无处可见。

当我在第 8 课介绍 if 语句时，这个概念的特定用法非常有用也不太令人困惑，所以我觉得现在讨论它只会有一点点内疚。

简而言之，变量是可容纳数据片段的命名内存块。要声明一个引用窗体实例的变量，你输入窗体的类型，后跟你想要赋予变量的任何名称。例如，以下代码声明了一个名为 newUserForm 的 MakeUserForm 类型变量：

```
MakeUserForm newUserForm;
```

在这一点上，程序有一个可以引用 MakeUserForm 对象的变量，但现在它不引用任何东西。它就像一个可以容纳 MakeUserForm 实例的空信封。在这一点上，变量包含特殊值 null，这基本上意味着它不引用任何东西。

你可以使用 new 关键字创建窗体类的新实例。然后你可以将变量设置为等于新的窗体实例。例如，以下代码创建一个新的 MakeUserForm 窗体并使 newUserForm 变量指向它：

```
newUserForm = new MakeUserForm();
```

现在变量引用了新的窗体。最后一步是显示新的窗体。你可以通过调用新窗体的 ShowDialog 或 Show 方法来实现。

> 注意 从技术上讲，变量并不保存或包含窗体。相反，它包含对窗体的引用。引用就像一个地址，指向窗体在内存中的实际位置。当你的代码说类似 newUserForm.Show() 的内容时，程序会找到实际的窗体实例并调用其 Show 方法。
> 
> 目前这种区别很小，你不必太担心它，但以后了解某些变量是实际保存其值的 value 类型（例如 int、long、double）而某些是保存其值引用的 reference 类型（例如控件、窗体，以及有趣的是 string）会很有用。
> 第 17 课在讨论结构时对此进行了更多说明。

ShowDialog 方法以模态方式显示窗体。这意味着窗体出现在程序其他窗体的顶部，并且用户在该窗体关闭之前无法与其它窗体交互。

这是对话框通常的工作方式。例如，当你打开“项目”菜单并选择“添加 Windows 窗体”时，“添加新项”对话框以模态方式显示，因此你无法在单击“添加”或“取消”关闭对话框之前与 IDE 的其他部分（例如“属性”窗口、解决方案资源管理器或菜单）交互。
