
(应用程序中的一个事件)。你需要设置 Label 控件的属性来自定义标签的外观。

让我们执行以下步骤在 WindowsControls 应用程序中使用 Label 控件：

1. 从工具箱拖动一个 Label 控件并将其放置在 Form1 表单的任意位置（图 C5.29）。
2. 从属性窗口将 Label 控件的 Text 属性设置为 Name，如图 C5.29 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_167_0.png)

在图 C5.29 中，Label 控件的文本更改为 Name。

## 使用 TextBox 控件

TextBox 控件是一个 Windows Forms 控件，允许你在运行时在表单上输入文本。此控件通常在用户需要简单的文本区域来显示一两行文本时使用。默认情况下，TextBox 控件仅接受单行文本。但是，通过设置 TextBox 控件的各种属性，你可以自定义它以接受多行文本，为控件添加滚动条，并禁用控件中的文本编辑。

让我们执行以下步骤在 WindowsControls 应用程序中使用 TextBox 控件：

1. 从工具箱拖动一个 TextBox 控件并将其放置在 Form1 表单上。
2. 双击本章“使用 Button 控件”部分中添加的 Click 按钮控件并添加清单 5.5 中给出的突出显示的代码：

### 清单 5.5：在 Button 控件的 button1_Click 事件上添加代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    textBox1.ForeColor = Color.Blue;
    textBox1.Text = "Hello C#";
    label1.BackColor = Color.Red;
}
```

在清单 5.5 中，ForeColor 属性用于定义 TextBox 控件的前景色。在我们的例子中，我们将其设置为蓝色。Text 属性用于定义 TextBox 控件中的文本。在我们的例子中，我们将其设置为“Hello C#”。BackColor 属性用于定义 Label 控件的背景色。在我们的例子中，我们将其设置为红色。

3. 按 F5 键运行 WindowsControls 应用程序。输出如图 C5.30 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_168_0.png)

图 C5.30

当你单击 Button 控件时，输出如图 C5.31 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_168_1.png)

图 C5.31

在图 C5.31 中，由于 ForeColor 属性，Label 控件的 BackColor 变为红色，TextBox 控件中的文本以蓝色显示。

## 使用 RichTextBox 控件

RichTextBox 控件用于显示、输入和操作带格式的文本。RichTextBox 控件与 TextBox 控件类似，只是 RichTextBox 控件允许你对输入其中的文本进行格式化。

让我们执行以下步骤在 Windows Forms 应用程序中使用 RichTextBox 控件：

1. 重复本章“更改表单标题”部分中的步骤 1 到 3。
2. 在名称文本框中输入 RichTextBoxControl 并在位置组合框中指定适当的位置。
3. 单击确定按钮。RichTextBoxControl 应用程序将以指定的名称和位置创建。
4. 从工具箱拖动一个 Button 控件并将其放置在 Form1 表单上（图 C5.32）。
5. 将 Button 控件的 Text 属性更改为 Click，如图 C5.32 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_168_2.png)

图 C5.32

6. 双击 Button 控件并在 Form1.cs 文件中添加清单 5.6 中显示的突出显示的代码：

### 清单 5.6：在 Click 按钮控件的 Click 事件上添加代码

```csharp
private void button1_Click(object sender, EventArgs e)
{
    RichTextBox richTextBox1 = new RichTextBox();
    richTextBox1.Dock = DockStyle.Top;
    richTextBox1.Height = 150;
    richTextBox1.Width = 50;
    this.Controls.Add(richTextBox1);
    richTextBox1.Text = "Hello! Welcome to the world of C# programming. This is the new version of C#.";
}
```

在清单 5.6 中，代码在 button1 的 Click 事件中添加了一个 RichTextBox 控件 richTextBox1。richTextBox1 的 Height 和 Width 属性分别设置为 150 和 50。此外，richTextBox1 的 Text 属性包含消息 Hello! Welcome to the world of C# programming. This is the new version of C#。

7. 按 F5 键运行 RichTextBoxControl 应用程序。输出出现（图 C5.33）。

8. 单击如图 C5.33 所示的 Click 按钮：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_169_0.png)

图 C5.33

输出如图 C5.34 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_169_1.png)

图 C5.34

在图 C5.34 中，Form1 表单上出现了一个带有一些文本的 RichTextBox 控件。

## 使用 RadioButton 控件

RadioButton 控件，也称为选项按钮，用于从一组选项中选择一个选项。此控件始终以组形式工作。这意味着每当你从一组 RadioButton 控件中选择一个 RadioButton 控件时，该组中的其他 RadioButton 控件会自动取消选择。RadioButton 控件可以显示文本、图像或两者兼有。

让我们执行以下步骤在 Windows Forms 应用程序中使用 RadioButton 控件：

1. 重复“更改表单标题”部分中的步骤 1 到 3。
2. 在名称文本框中输入 ControlApplication 并在位置组合框中指定适当的位置。
3. 单击确定按钮。ControlApplication Windows Forms 应用程序将以指定的名称和位置创建。

4. 从工具箱拖动三个 RadioButton 控件和一个 Label 控件并将其放置在 Form1 表单上（图 C5.35）。

5. 在属性窗口中将 radioButton1 的 Text 属性设置为 Red，如图 C5.35 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_170_0.png)

图 C5.35

6. 从属性窗口更改 radioButton2 的 Text 属性为 Blue，radioButton3 为 Green，label1 为 Welcome。

7. 双击 Red 单选按钮并在 Red 单选按钮的 CheckedChanged 事件上添加清单 5.7 中显示的突出显示的代码：

### 清单 5.7：在 Red 单选按钮的 CheckedChanged 事件上添加代码

```csharp
private void radioButton1_CheckedChanged(object sender, EventArgs e)
{
    label1.ForeColor = Color.Red;
}
```

在清单 5.7 中，当你选择 Red 单选按钮时，label1 标签的前景色会使用其 ForeColor 属性更改为红色。

8. 在 Blue 单选按钮的 CheckedChanged 事件上添加清单 5.8 中显示的突出显示的代码：

### 清单 5.8：在 Blue 单选按钮的 CheckedChanged 事件上添加代码

```csharp
private void radioButton2_CheckedChanged(object sender, EventArgs e)
{
    label1.ForeColor = Color.Blue;
}
```

在清单 5.8 中，当你选择 Blue 单选按钮时，标签的字体颜色会使用 label1 控件的 ForeColor 属性更改为蓝色。

9. 在 Green 单选按钮的 CheckedChanged 事件上添加清单 5.9 中显示的突出显示的代码：

### 清单 5.9：在 Green 单选按钮的 CheckedChanged 事件上添加代码

```csharp
private void radioButton3_CheckedChanged(object sender, EventArgs e)
{
    label1.ForeColor = Color.Green;
}
```

在清单 5.9 中，当你选择 Green 单选按钮时，标签的字体颜色会使用 label1 控件的 ForeColor 属性更改为绿色。

10. 按 F5 键运行 ControlApplication 应用程序并选择三个单选按钮中的任意一个。在我们的例子中，我们选择了 Blue 单选按钮。输出如图 C5.36 所示：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_171_0.png)

在图 C5.36 中，当选择 Blue 单选按钮时，标签的前景色更改为蓝色。

## 使用 CheckBox 控件

CheckBox 控件接受 true 或 false 的值。你只需单击 CheckBox 控件即可选择它。当 CheckBox 控件被选中时会出现一个复选标记；再次单击控件即可取消选择它。当你选择 CheckBox 控件时，它保存值 true，而当你取消选择 CheckBox 控件时，它保存值 false。CheckBox 控件可以显示与其关联的图像或相应文本。它也可以同时显示两者。

让我们执行以下步骤在 ControlApplication 应用程序中使用 CheckBox 控件：

1. 从工具箱拖动两个 CheckBox 控件并将其放置在 Form1 表单上（图 C5.37）。
2. 在属性窗口中将 checkBox1 的 Text 属性设置为 Bold，如图 C5.37 所示：
3. 在属性窗口中将 checkBox2 的 Text 属性更改为 Italic。
4. 双击复选框 Bold 并在 checkBox1 的 CheckedChanged 事件上添加清单 5.10 中显示的突出显示的代码：

![](img/2db4b8b2cb67e7ccc52477a61fe289ab_171_1.png)

### 清单 5.10：在 checkBox1 的 CheckedChanged 事件上添加代码

```csharp
private void checkBox1_CheckedChanged(object sender, EventArgs e)
{
    label1.Font = new Font(label1.Font.Name, label1.Font.Size, label1.Font.Style |
        FontStyle.Bold);
}
```

在清单 5.10 中，代码在你选择 Bold 复选框时将 label1 标签上显示的文本的字体更改为粗体。

5. 在 checkBox2 的 CheckedChanged 事件上添加清单 5.11 中显示的突出显示的代码：

### 清单 5.11：在 checkBox2 的 CheckedChanged 事件上添加代码

```csharp
private void checkBox2_CheckedChanged(object sender, EventArgs e)
{
```
