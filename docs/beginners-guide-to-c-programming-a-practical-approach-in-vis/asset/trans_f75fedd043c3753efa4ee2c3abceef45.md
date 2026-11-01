
```csharp
private void Form1_Load(object sender, EventArgs e)
{
    incrementProgressBar.Minimum = 0;
    incrementProgressBar.Maximum = 100;
    incrementProgressBar.Step = 1;
}
```

代码 5.22

- 7. 双击按钮并创建其单击事件处理方法。

每次用户单击按钮时，ProgressBar 的值将增加 1。当前值也会添加到 ListBox 的项目中。以下代码执行此操作：

```csharp
private void incrementButton_Click(object sender, EventArgs e)
{
    incrementProgressBar.Value += 1;
    currentValueListBox.Items.Add(incrementProgressBar.Value);
}
```

代码 5.23

代码行 `incrementProgressBar.Value += 1;` 将 1 加到 incrementProgressBar 的 Value 属性上。下一行获取 ProgressBar 的 Value 并将其传递给 Add() 方法，该方法将此 Value 添加到 ListBox。

- 8. 让我们构建并运行项目。最初，我们的程序将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_115_0.png)

图 5.85. 单击“递增”按钮之前的程序

单击按钮几次后，ProgressBar 将被填满，其值将写入 ListBox 如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_116_0.png)

图 5.86. ProgressBar 为 21%

## 5.16. 单选按钮

RadioButton 用于在不同选项中进行选择。

> RadioButton 类似于 CheckBox，然而在一个窗体或组中一次只能选择一个 RadioButton。

RadioButton 经常使用的属性如下：

- **Checked:** 设置 RadioButton 是否初始被选中。
- **AutoCheck:** 设置 RadioButton 在被单击时是否自动被选中。
- **Enabled:** 设置 RadioButton 是否可供选中。

以下简单示例演示了项目中 RadioButton 的使用。用户将使用 RadioButton 选择窗体的背景颜色。由于不能同时将背景颜色设置为多种颜色，因此在此示例中使用 RadioButton 是有意义的。

- 1. 在 Visual Studio 中创建一个新的 C# 项目。
- 2. 在窗体上添加五个 RadioButton，如下所示：

```csharp
private void whiteRadioButton_CheckedChanged(object sender, EventArgs e)
{
    this.BackColor = Color.White;
}

private void brownRadioButton_CheckedChanged(object sender, EventArgs e)
{
    this.BackColor = Color.Brown;
}
```

代码 5.24（续）

如前所述，this.BackColor 指的是窗体的背景颜色。因此，在此代码片段中，每个 RadioButton 都为窗体的背景分配不同的颜色。

- 6. 构建并运行项目。由于第一个 RadioButton 默认会被选中，因此窗体的背景颜色初始为红色，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_118_0.png)

图 5.88. 程序的初始状态

当我们选中不同的 RadioButton 时，窗体的背景颜色将相应改变，如图 5.89 所示。

当可选选项具有单一且离散的性质时，使用 RadioButton 是很有用的。

![](img/41d82527c4e41cdb7e56259564306ddc_119_0.png)

图 5.89. 选择白色 RadioButton 时的程序

## 5.17. 富文本框

RichTextBox 用于输入具有段落和多行文本格式等格式功能的文本。RichTextBox 的重要属性如下：

- **DetectUrls**: 设置是否自动将 URL 转换为链接。
- **MultiLine**: 设置是否允许多行文本输入。
- **MaxLength**: 可在 RichTextBox 中输入的字符数。

在我们的示例中，我们将在窗体上放置一个 RichTextBox。当我们单击按钮时，RichTextBox 中输入的文本将显示在消息框中。

- 1. 在 Visual Studio 中创建一个新的 C# 项目。
- 2. 在窗体上放置一个 RichTextBox 和一个 Button，如图 5.90 所示。
- 3. 将 RichTextBox 的 Name 设置为 **inputRichTextBox**。
- 4. 将 Button 的 Name 和 Text 分别设置为 **showButton** 和 **Show in MessageBox**。
- 5. 双击 Button 以创建其事件处理方法 **showButton_Click()**。
- 6. 在此方法中添加代码 `MessageBox.Show(inputRichTextBox.Text);`。

![](img/41d82527c4e41cdb7e56259564306ddc_120_0.png)

图 5.90. 窗体的布局

```csharp
private void showButton_Click(object sender, EventArgs e)
{
    MessageBox.Show(inputRichTextBox.Text);
}
```

代码 5.24

- 7. 让我们构建并运行项目。我们可以在 RichTextBox 中输入格式化的文本。当我们单击“显示在消息框中”按钮时，RichTextBox 中输入的文本将显示在消息框中。请注意，文本的格式在消息框中显示时得以保留。

![](img/41d82527c4e41cdb7e56259564306ddc_120_1.png)

图 5.91. 在消息框中显示格式化的文本

## 5.18. 文本框

TextBox 可能是 Windows Forms 应用程序中仅次于 Button 最常用的控件。TextBox 简单用于从用户收集文本输入。它具有以下重要属性：

- **MultiLine**: 设置文本输入是否可跨越多行。
- **WordWrap**: 如果文本超出单行，则会自动换行到下一行。
- **ScrollBars**: 设置文本滚动条是否可见。

在我们的示例中，我们将从多个 TextBox 收集文本并在添加到 ListBox 之前合并它们。

- 1. 在 Visual Studio 中创建一个新的 C# 项目。
- 2. 在窗体上放置三个 Label、三个 TextBox、一个 Button 和一个 ListBox，如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_121_0.png)

图 5.92. 窗体的布局

- 3. 从上到下将 Label 的 Texts 设置为 **Name:**、**Lesson:** 和 **Grade:**。
- 4. 从上到下将 TextBox 的 Name 属性设置为 **nameTextBox**、**lessonTextBox** 和 **gradeTextBox**。
- 5. 分别将 Button 的 Text 和 Name 设置为 **Add Info** 和 **addInfoButton**。
- 6. 将 ListBox 的 Name 设置为 **infoListBox**。进行这些更改后，窗体将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_122_0.png)

图 5.93. 更改后的窗体布局

- 7. 当单击“添加信息”按钮时，将读取 TextBox 的 Texts、合并并添加到 ListBox。为此，通过双击它创建按钮的默认事件处理程序 addInfoButton_Click(...) 并添加以下代码：

```csharp
private void addInfoButton_Click(object sender, EventArgs e)
{
    infoListBox.Items.Add(nameTextBox.Text + "-" + lessonTextBox.Text + "-" + gradeTextBox.Text);
    nameTextBox.Clear();
    lessonTextBox.Clear();
    gradeTextBox.Clear();
}
```

代码 5.26

在第一行中，合并后的文本被传递给 Add() 方法以执行向 ListBox 的添加操作。在此操作中，+ 运算符合并文本。此外，文本之间放置了连字符（-）。值得注意的是，连字符写在双引号内，以告诉 Visual Studio 将连字符视为文本。

将合并后的文本添加到 ListBox 后，通过应用 Clear() 方法清除 TextBox。因此，所有 TextBox 在无需用户干预的情况下被清除，使其准备好输入新输入。

- 8. 现在我们可以构建并运行项目。当我们向 TextBox 输入文本并单击按钮时，这些文本将被合并并添加到 ListBox，如图 5.94 所示。

> 请注意，TextBox 中写入的文本被视为文本（字符串）。因此，在将这些输入写入 ListBox 时，我们不需要进行任何转换。

![](img/41d82527c4e41cdb7e56259564306ddc_123_0.png)

图 5.94. 使用 TextBox 进行文本输入（新条目尚未添加到 ListBox）

## 5.19. 工具提示

ToolTip 用于为窗体上的控件添加提示（小信息）。当鼠标指针位于关联控件上方时，其 ToolTip 被激活并显示相关信息。

ToolTip 常用属性如下：

- **InitialDelay**: 鼠标指针停留在控件上以使 ToolTip 显示信息所需的时间。
- **ToolTipIcon**: 指定将与信息一起显示的图标。
- **IsBalloon**: 设置信息是否在气球内显示。
