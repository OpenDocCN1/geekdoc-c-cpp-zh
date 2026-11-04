
创建带有按钮的 `ToolStrip`，这些按钮复制菜单层次结构。`ToolStrip` 应包含两个 `ToolStripDropDownButton`。

将第一个工具命名为 `foreColorButton`，并使其显示文本“A.”。为其提供 Black、Red、Green 和 Blue 项。每个项的 `ForeColor` 属性都应设置为其颜色。

- 1. 创建 `ToolStripDropDownButton`。
- 2. 在该项下方，添加 Black、Red、Green 和 Blue 项。
- 3. 为这些项分别设置 `ForeColor` 属性以显示其颜色。（例如，将 Black 项的 `ForeColor` 属性设置为黑色。）

将第二个工具命名为 `backColorButton`，并使其初始显示白色颜色示例。为其提供 White、Pink、Light Green 和 Light Blue 项。使这些项分别显示一个展示该颜色示例的 `Image`。

- 1. 创建 `ToolStripDropDownButton`。
- 2. 在该项下方，添加 White、Pink、Light Green 和 Light Blue 项。
- 3. 为这些项分别设置 `Image` 属性以显示其颜色示例。

为 `StatusStrip` 提供一个名为 `colorLabel` 的 `ToolStripStatusLabel`，其 Text = "Text Colors"。

- 1. 创建 `ToolStripStatusLabel`。设置其 Name 和 Text 属性。

添加事件处理程序。

使文件菜单的 Exit 项关闭窗体。

- 1. 键入粗体代码行，使事件处理程序如下所示：

```csharp
private void fileExitMenuItem_Click(object sender, EventArgs e)
{
    Close();
}
```

为每个 Text Color 菜单项创建事件处理程序。

- 1. 对于 Text Color Black 菜单项，键入粗体代码，使事件处理程序如下所示：

```csharp
private void blackForeColorMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.ForeColor = blackForeColorButton.ForeColor;
    foreColorMenuItem.ForeColor = blackForeColorButton.ForeColor;
    foreColorButton.ForeColor = blackForeColorButton.ForeColor;
    colorLabel.ForeColor = blackForeColorButton.ForeColor;
    blackForeColorMenuItem.Checked = true;
    redForeColorMenuItem.Checked = false;
    greenForeColorMenuItem.Checked = false;
    blueForeColorMenuItem.Checked = false;

    blackForeColorButton.Checked = true;
    redForeColorButton.Checked = false;
    greenForeColorButton.Checked = false;
    blueForeColorButton.Checked = false;
}
```

- 2. 为其他 Text Color 菜单项输入类似代码。

- 为每个 Background Color 菜单项创建事件处理程序。

  - 1. 对于 Background Color ▸ White 菜单项，键入粗体代码，使事件处理程序如下所示：

```csharp
private void whiteBackColorMenuItem_Click(object sender, EventArgs e)
{
    contentRichTextBox.BackColor = Color.White;

    backColorMenuItem.Image = whiteBackColorMenuItem.Image;
    backColorButton.Image = whiteBackColorMenuItem.Image;
    colorLabel.BackColor = Color.White;

    whiteBackColorMenuItem.Checked = true;
    pinkBackColorMenuItem.Checked = false;
    lightGreenBackColorMenuItem.Checked = false;
    lightBlueBackColorMenuItem.Checked = false;

    whiteBackColorButton.Checked = true;
    pinkBackColorButton.Checked = false;
    lightGreenBackColorButton.Checked = false;
    lightBlueBackColorButton.Checked = false;
}
```

  - 2. 为其他 Background Color 菜单项输入类似代码。

- 为每个 Background Color 菜单项创建事件处理程序。

  - 1. 重复你为 Text Color 菜单项使用的步骤，但使用 BackColor 而不是 ForeColor。

- 使工具条按钮使用对应菜单项的事件处理程序。

  - 1. 单击属性窗口的 Events 按钮。
  - 2. 对于每个工具条按钮：
    - a. 在窗体编辑器中单击该按钮。
    - b. 在属性窗口中，选择 Click 事件。然后单击右侧的下拉箭头。
    - c. 选择相应的菜单事件处理程序。例如，对于 blackForeColorButton 工具条按钮，选择 blackForeColorMenuItem_Click 事件处理程序。

## 练习

### 1. [SimpleEdit]

复制你在第 5 课练习 10 中构建的 SimpleEdit 程序（或从本书网站下载第 5 课的版本），并添加图 6-7 中所示的工具条、按钮和分隔符。提示：

- 删除 RichTextBox 控件，添加 ToolStripContainer，然后在 ToolStripContainer 的内容面板中重新添加 RichTextBox。然后添加 ToolStrip。
- 黑色按钮（第三行工具条中从左数第四个）是一个 ToolStripSplitButton，允许用户选择文本颜色。它包含选项 Black、White、Red、Green 和 Blue。
- 文本颜色按钮旁边的白色按钮是另一个 ToolStripSplitButton，允许用户选择背景色。它包含选项 Black、White、Pink、Light Green、Light Blue 和 Yellow。
- 显示“AB”的按钮是一个 ToolStripDropDownButton，提供与 Format 菜单的 Offset 子菜单相同的选项：Normal、Superscript 和 Subscript。

![](img/d5be6ade75773ca6cec5c78f96a98bb1_137_0.png)

### 2. [WPF, SimpleEdit]

复制你在第 5 课练习 12 中构建的程序（或从本书网站下载第 5 课的版本），并重复练习 1。提示：

- 将 ToolBarTray 停靠到菜单下方 DockPanel 控件的顶部。
- 将 ToolBar 添加到 ToolBarTray。设置 ToolBar 的 Band 属性以指示其在 ToolBarTray 中的行。设置其 BandIndex 属性以指示其在带区内的顺序。
- 将 Button 和 Separator 添加到 ToolBar。
- 对于拆分按钮，使用包含 ComboBoxItem 的 ComboBox，这些 ComboBoxItem 包含 Image。将某个 ComboBoxItem 的 IsSelected 属性设置为 True，以设置 ComboBox 的初始选择。
- 将 StatusBar 停靠到 DockPanel 的底部。为其提供一个包含 Label 的 StatusBarItem。

### 3. [SimpleEdit]

复制你为练习 1 构建的 SimpleEdit 程序，并添加菜单项代码以管理新的工具条按钮。添加代码以同步对应的菜单项、上下文菜单项和工具条按钮项。例如，下面显示了 Align Left 菜单项的新代码：

```csharp
private void formatAlignLeftMenuItem_Click(object sender, EventArgs e)
{
    formatAlignLeftMenuItem.Checked = true;
    formatAlignRightMenuItem.Checked = false;
    formatAlignCenterMenuItem.Checked = false;
    alignLeftContextMenuItem.Checked = true;
    alignRightContextMenuItem.Checked = false;
    alignCenterContextMenuItem.Checked = false;
    alignLeftButton.Checked = true;
    alignRightButton.Checked = false;
    alignCenterButton.Checked = false;
    MessageBox.Show("Align Left");
}
```

### 4. [WPF, SimpleEdit]

使用你为练习 2 构建的 WPF 应用程序重复练习 3。提示：

- 在 WPF 中，Button 没有 Checked 或 IsChecked 属性，因此无法选中和取消选中对齐工具栏按钮。请改为创建单独的图像来表示选中和未选中状态。将选中和未选中的图像放入 Image 控件中，并将 Visibility 属性设置为 Collapsed。然后使用类似下面的代码在运行时设置 Button 的图像：

  `alignLeftImage.Source = alignLeftUncheckedImage.Source;`

- 对项目符号按钮使用类似的技巧。使用类似下面的代码设置按钮的 Image 属性。（抱歉，我想不出不使用 if-else 语句就能轻松处理此问题的方法，你将在第 18 课学习 if-else 语句。）

  ```csharp
  if (formatBulletMenuItem.IsChecked)
      bulletImage.Source = bulletCheckedImage.Source;
  else
      bulletImage.Source = bulletUncheckedImage.Source;
  ```

- 要处理偏移量工具栏项，请为偏移量 ComboBoxItem 命名。然后按下述代码设置选定项。（对于未选中的项，不需要将其设置为 false。）

  `superscriptOffsetComboBoxItem.IsSelected = true;`

- 使用与处理偏移量 ComboBox 相同的方式处理缩进工具栏 ComboBox。

### 5. [SimpleEdit]

复制你为练习 3 构建的 SimpleEdit 程序，并将工具条控件附加到对应的事件处理程序。（暂时不必担心颜色控件。）

### 6. [WPF, SimpleEdit]

使用你为练习 4 构建的 WPF 应用程序重复练习 5。提示：

- 处理偏移量和缩进 ComboBoxItem 的 Selected 事件。
- 窗口加载时，会为最初选中的 ComboBoxItem 引发 Selected 事件。不幸的是，窗口尚未完成所有控件的加载，如果程序尝试为尚未加载的控件设置值，就会崩溃。为防止这种情况，请使用以下语句开始最初选中的 ComboBoxItem 的事件处理程序。（该语句基本上意味着：“如果窗口尚未加载，则退出事件处理程序。”）

  `if (!IsLoaded) return;`

- 你可能会注意到，如果你选择对应的菜单项或上下文菜单项之一，ComboBoxItem 事件处理程序会执行两次。这有点低效，但暂时不必担心。我们稍后会修复它。

