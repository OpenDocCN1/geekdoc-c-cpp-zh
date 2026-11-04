
这会让 ListBox 移除当前选中的项。幸运的是，如果没有选中项，ListBox 不会崩溃，而是什么都不做。

当用户点击对话框的“取消”按钮时，隐藏对话框并返回 DialogResult.Cancel。

- 1. 你不需要做其他任何事情就能让它工作。当你将对话框的 CancelButton 属性设置为此按钮时，C# 会将按钮的 DialogResult 属性设置为 DialogResult.Cancel，因此按钮会自动设置返回结果并关闭对话框。

当用户点击对话框的“确定”按钮时，检查输入名称的长度。如果长度为 0，显示一条消息要求用户输入名称。如果长度大于 0，隐藏对话框并返回 DialogResult.OK。

- 1. 为对话框的“确定”按钮创建一个事件处理程序。使用类似下面的代码：

```csharp
// Make sure the comedian's name isn't blank.
private void okButton_Click(object sender, EventArgs e)
{
    if (nameTextBox.Text.Length == 0)
    {
        MessageBox.Show("Please enter a comedian's name");
    }
    else
    {
        DialogResult = DialogResult.OK;
    }
}
```

## 练习

- 1. [WPF] 使用 WPF 应用程序重复“试一试”练习。提示：

```csharp
if (newComedianDialog.ShowDialog().Value)
{
    ...
}
```

  - 要查看用户是否在对话框上点击了“确定”，请查看 ShowDialog 方法是否返回 True，如上面的代码所示：
  - 要定义“接受”按钮，请将按钮的 IsDefault 属性设置为 True。
  - 要定义“取消”按钮，请将按钮的 IsCancel 属性设置为 True。
  - 要关闭对话框，“确定”按钮的代码应设置 DialogResult = true。
  - 要防止用户调整对话框大小，请将 ResizeMode 设置为 NoResize。
  - 要防止对话框出现在任务栏中，请将 ShowInTaskbar 设置为 False。

- 2. 通常，阻止用户执行无效操作比允许用户执行操作后再抱怨要好。在“试一试”中，即使没有选中任何喜剧演员，用户也可以单击“删除喜剧演员”按钮。要修复这个问题，请复制你为“试一试”构建的程序，并添加以下事件处理程序，以便在 ListBox 的选择发生变化时启用或禁用该按钮：

```csharp
// Enable the Delete Comedian button if an entry is selected.
private void comedianListBox_SelectedIndexChanged(
    object sender, EventArgs e)
{
    deleteComedianButton.Enabled =
        (comedianListBox.SelectedIndex >= 0);
}
```

提示：不要忘记在初始时禁用该按钮。

- 3. [WPF] 使用你在练习 1 中构建的 WPF 程序重复练习 2。（提示：在 WPF 中，Button 具有 IsEnabled 属性，而不是 Enabled 属性。）

- 4. 复制你在练习 2 中构建的程序。为了进一步帮助用户避免犯错，修改对话框，使“确定”按钮在 TextBox 中的文本非空时启用。提示：
  - 使用 TextBox 的 TextChanged 事件处理程序。
  - 因为当文本为空白时用户无法点击“确定”按钮，所以“确定”按钮不需要 Click 事件处理程序。只需将其 DialogResult 属性设置为 OK。

- 5. [WPF] 使用你在练习 3 中构建的 WPF 程序重复练习 4。（提示：在 WPF 中，Button 没有 DialogResult 属性。“确定”按钮仍然需要 Click 事件处理程序，但它只需要设置窗体的 DialogResult 属性。）

- 6. 创建一个程序，具有“名字”、“姓氏”、“街道”、“城市”、“州”和“邮政编码”标签，如图 10-3 中的“联系信息”窗体所示。当用户点击“编辑”按钮时，程序应显示图 10-3 中所示的“编辑联系人”对话框，让用户更改这些值。如果用户点击“确定”，则将新值复制回主窗体的标签中。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_193_0.png)

图 10-3

- 7. [WPF] 使用 WPF 应用程序重复练习 6。

- 8. 有时，MessageBox.Show 提供的标准消息框几乎完美，但你可能想要更改按钮的文本。创建一个程序，定义如图 10-4 所示的消息对话框。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_194_0.png)

图 10-4

主程序应设置标签的文本、对话框的标题以及按钮的文本。让“接受”按钮返回 DialogResult.OK，让“拒绝”按钮返回 DialogResult.Cancel。让主窗体显示不同的消息，具体取决于用户点击的是“接受”还是“拒绝”。

提示：
  - 问号图标显示在 PictureBox 中。
  - 设置对话框的属性：FormBorderStyle = FixedDialog、ControlBox = False 和 ShowInTaskbar = False。

- 9. [WPF] 使用 WPF 程序重复练习 8。提示：
  - 要设置对话框的标题，请设置其 Title 属性。
  - WPF 的 Label 控件不支持自动换行。要让对话框换行，请使用 TextWrapping 设置为 Wrap 的 TextBlock。

- 10. 创建一个颜色选择对话框，如图 10-5 所示。主程序的按钮应显示相同的对话框，让用户选择前景色和背景色。仅当用户点击“确定”时才更新主窗体的颜色。在显示对话框之前，无需担心将其初始化为显示当前值。（提示：你在第 4 课的“试一试”中构建了一个让用户通过滚动条选择颜色的程序。）

![](img/d5be6ade75773ca6cec5c78f96a98bb1_194_1.png)

图 10-5

- 11. [WPF] 使用 WPF 程序重复练习 10。提示：
  - 在 Border 控件中显示颜色样本。
  - 让 ScrollBars 共享以下事件处理程序：

```csharp
// Display the color sample.
private void redScrollBar_Scroll(object sender,
    System.Windows.Controls.Primitives.ScrollEventArgs e)
{
    redLabel.Content = redScrollBar.Value.ToString("0");
    greenLabel.Content = greenScrollBar.Value.ToString("0");
    blueLabel.Content = blueScrollBar.Value.ToString("0");

    Color color = Color.FromRgb(
        (byte)redScrollBar.Value,
        (byte)greenScrollBar.Value,
        (byte)blueScrollBar.Value);
    sampleBorder.Background = new SolidColorBrush(color);
}
```

- 12. 创建一个背景选择对话框，如图 10-6 所示。当用户点击主窗体的“选择背景”按钮时，窗体显示该对话框。当用户点击某个缩略图时，对话框会在该图片的 PictureBox 周围显示边框。如果用户点击“确定”，对话框关闭，主窗体以全尺寸显示所选图像。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_195_0.png)

图 10-6

提示：
  - 当用户点击图像时，将该 PictureBox 的 BorderStyle 属性设置为 Fixed3D，其他 PictureBox 设置为 None。
  - 要记住选择了哪个图像，请在对话框上放置一个隐藏的 PictureBox，并将其 Image 属性设置为被点击的 PictureBox 的 Image 属性。
  - 使用第 9 课练习 18 中描述的技术，为所有四个 PictureBox 使用一个事件处理程序。
  - 仅当已选择图片时才允许用户点击对话框的“确定”按钮。
  - 如果用户点击“确定”，调整主窗体大小以适应新的背景图像。
  - 将“取消”按钮的 TabStop 属性设置为 False。（要了解原因，请将其设置为 True，运行程序，选择一张图片，然后按 Enter。）

- 13. 使用 WPF 应用程序重复练习 12。提示：
  - 在主窗口上放置一个 Image 控件，并在其中显示选中的图片。
  - 不用担心调整主窗口大小以适应选中的图片。
  - 在 WPF 中，Image 控件没有 BorderStyle 属性。通过将所选 Image 控件的 Opacity 属性设置为 1 来表示选中。将其他 Image 控件的 Opacity 属性设置为 0.5。

> 注意：请在线选择第 10 课的视频，网址为 www.wrox.com/go/csharp24hourtrainer2videos。

## 第二部分

## 变量与计算

你可能已经注意到，到目前为止的课程中，除了简单地显示文本之外，并没有涉及太多关于数字、日期、文本或其他数据的内容。这些课程主要处理控件及其属性、方法和事件。

尽管仅使用控件就能完成一些相当令人印象深刻的事情，但大多数程序还需要处理数据。它们需要做的事情包括：累加采购成本、计算销售税、按时间对约会进行排序，以及在文本中搜索关键词。

本节中的课程将解释如何执行这些类型的任务。它们解释了程序在代码中用来表示数据的变量，并展示了如何操作变量来计算新的结果。

- 第 11 课：使用变量和执行计算
- 第 12 课：调试代码
- 第 13 课：理解作用域
- 第 14 课：处理字符串
- 第 15 课：处理日期和时间
- 第 16 课：使用数组和集合
- 第 17 课：使用枚举和结构
