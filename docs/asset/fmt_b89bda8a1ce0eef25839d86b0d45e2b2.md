
## 练习

- 在按钮的 `Click` 事件处理器中，将两个定时器的 `Enabled` 设置为 `false`。

运行程序。尝试定时器 `Interval` 属性的不同取值。如果 `Interval = 10`，会发生什么？

### 6.
复制你为练习 1 构建的 `FollowMouse` 程序。修改副本，使使用户可以通过调整滚动条来移动 `PictureBox`。

### 7. [WPF]
复制你为练习 2 构建的程序。修改该副本，使用户能够调整滚动条来移动图像。（提示：保存代码，对两个滚动条都使用事件处理程序。为了防止鼠标出现在滚动条和窗口右下角的小区域上方，将 `Canvas` 控件的 `ClipToBounds` 属性设置为 `True`。）

### 8.
创建一个与图 4-5 所示类似的程序。当用户勾选早餐 `Breakfast`、午餐 `Lunch` 或晚餐 `Dinner` 复选框时，程序应该禁用对应的 `GroupBox`。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_107_0.png)

FIGURE 4-5

提示：

- 将 `OK` 按钮设置为单的接受按钮 `accept button`。将 `Cancel` 按钮设置为表单的取消按钮 `cancel button`。

- 放空 `GroupBoxes` 的 `Text` 属性。将 `CheckBoxes` 放置在 `GroupBoxes` 之上，位于文本所在的位置。（确保不要将 `CheckBoxes` 放置在 `GroupBoxes` 内部。尝试查看为什么不起作用。你可能需要先定位 `CheckBoxes`，然后将 `GroupBoxes` 移动到位置。）

- 要启用或禁用 `GroupBox`，在下面的代码中将其 `Enabled` 属性设置为对应 `CheckBox` 的 `Enabled` 属性：

```sharp
// 启用或禁用对应的 GroupBox.
private void breakfastCheckBoxCheckedChanged(object sender, EventArgs e)
{
    breakfastGroupBox.Enabled = breakfastCheckBox.Checked;
}
```

### 9. [WPF]
使用 WPF 重复练习 8。

- WPF 的 `CheckBox` 不显示背景，因此此程序中的复选框不会覆盖周围的 `GroupBox` 边框。为了解决这个问题，将每个 `CheckBox` 放置在一个 `Canvas` 中，并让 `Canvas` 使用白色背景。

- `GroupBox` 只能有一个子元素。给每个 `GroupBox` 提供一个包含 `RadioButtons` 的 `StackPanel`。使用 `RadioButtons` 的 `Margin` 属性在选项之间添加一些间距。

WPF 的 `CheckBox` 没有 `CheckChanged` 事件。请使用 `Click` 事件代替。

要启用或禁用 `GroupBox`，如下面的代码所示，将其 `IsEnabled` 属性设置为等于对应 `CheckBox` 的 `IsChecked.Value` 属性：

```csharp
// 启用或禁用相应的 GroupBox.
private void breakfastCheckBox_Click(object sender, RoutedEventArgs e)
{
    breakfastGroup.IsEnabled = breakfastCheckBox.Checked;
}
```

要设置 WPF 窗口的接受按钮，将按钮的 `IsDefault` 属性设置为 `True`。

要设置 WPF 窗口的取消按钮，将按钮的 `IsCancel` 属性设置为 `True`。

### 10.
创建一个与图 4-6 所示类似的程序。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_108_0.png)

FIGURE 4-6

- 创建一个 `PictureBox` 并向其中加载一张图像。将其大小设置为与图片大小匹配，并将其 `ScaleMode` 属性设置为 `StretchImage`。（同时也看看如果将其设置为 `Normal` 会发生什么。）

- 将滚动条放置在 `PictureBox` 旁边。设置它们的 `Maximum` 属性，以便使用户可以在 0 和图片的宽度/高度之间选择值。

- 初始时将滚动条的 `Value` 属性设置为图像的宽度/高度。

- 让滚动条的 `Scroll` 事件处理程序将 `PictureBox` 的宽度/高度设置为滚动条的值。

### 11. [WPF]
使用 WPF 重复练习 10。提示：

- 将 `Image` 控件的 `Stretch` 属性设置为 `Fill`。（同时也看看如果将其设置为 `None` 会发生什么。）

- 在 WPF 程序中，用户可以使用 `ScrollBar` 将其滑动到 `Maximum` 值。

### 12. [WPF, 游戏, 困难]
在 Windows Forms 应用中必须做的一件但在 WPF 应用中很容易实现（至少如果你设置得当的话）的事情是转换对象。例如，缩放、旋转和倾斜控件是相对容易的。对于这个练习，创建一个与图 4-7 所示类似的程序。当用户调整底部的滚动条时，程序应该旋转图像并在右下角的 `Label` 中显示旋转角度。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_109_0.png)

FIGURE 4-7

提示：

- 布局窗口及其控件。在 `Image` 控件中放入一张图片。将标签控件命名为 `degreesLabel`。

- 使用窗口的 `Transform` 部分将 `Image` 旋转 360 度。编辑 XAML 代码，为 `rotateTransform` 一个名为 `x:Name` 的属性。`Image` 控件的代码应该如下：

```xml
<Image x:Name="image" HorizontalAlignment="Left" VerticalAlignment="Top" Source="ScienceGirl.png" Stretch="Grid" Margin="10,10,0,0" RenderTransform="0.5,0.5">
  <TransformGroup>
    <ScaleTransform/>
    <SkewTransform/>
    <RotateTransform x:Name="rotateTransform" Angle="360"/>
    <TranslateTransform/>
  </TransformGroup>
</Image>
```

- 让 `ScrollBar` 的 `ValueChanged` 事件处理程序看起来如下所示：

```csharp
private void degreesScrollBar_ValueChanged(object sender, RoutedPropertyChanged<double> e)
{
  rotateTransform.Angle = degreesScrollBar.Value;
  degreesLabel.Content = degreesScrollBar.Value.ToString("0");
}
```

### 13. [WPF]
使用 WPF 应用重复练习 10。提示：

- 将 `Image` 控件的 `Stretch` 属性设置为 `Fill`。（同时也看看如果将其设置为 `None` 会发生什么。）

- 在 WPF 程序中，用户可以使用 `ScrollBar` 将其滑动到 `Maximum` 值。

### 2. [WPF, 游戏, 困难]
在 Windows Forms 应用中必须做的一件但在 WPF 应用中很容易实现（至少如果你设置得当的话）的事情是转换对象。例如，缩放、旋转和倾斜控件是相对容易的。对于这个练习，创建一个与图 4-7 所示类似的程序。当用户调整底部的滚动条时，程序应该旋转图像并在右下角的 `Label` 中显示旋转角度。

# 第 5 节 制作菜单

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_113_0.png)

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_113_1.png)

图 5-2

图 5-1

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_113_2.png)

图 5-3

你可以在此使用 `Offset`（偏移量）创建任意深度的子菜单，但在实际操作中，三级（如编辑 `Offset Offset Subscript`）已经是用户能够接受的极限。

除了菜单项外，你还可以在菜单中放置分隔符 `Separators`、文本框 `TextBox` 和组合框 `ComBoxes`。文本框和组合框在菜单中并不常见，因此我在这里不会介绍它们。然而，分隔符对于分组相关项目非常有用。

要创建分隔符，请右键点击某个项，打开“插入”子菜单并选择“分隔符”。或者，你可以创建一个普通的菜单项并将其文本设置为单个横杠 `-`。

www.it-ebooks.info

## 设置菜单属性

菜单中的项是 `ToolStripMenuItems`，与其他控件一样，它们拥有决定其外观和行为的属性。表 5-1 总结了最有用的 `ToolStripDropDownItem` 属性。

表 5-1

| 属性 | 目的 |
| --- | --- |
| Checked | 决定项目是否被选中。在图 5-3 中，`Normal` 项是选中的。（另请参见 `CheckOnClick`。） |
| CheckOnClick | 如果设置为 `True`，当用户选择该项目时，该项目会自动切换其选中状态。 |
| Enabled | 表示该项目是否可用。 |
| Name | `ToolStripMenuItem` 的名称。通常情况下，你应该为你的项目起一个好名字，以便在需要时通过它让程序执行某些操作。 |
| Shortcuts | 表示该项目的快捷键组合（如果有）。你可以输入如 `Ctrl+N` 这样的值，或者点击右侧的下拉箭头以显示图 5-4 所示的快捷键编辑器。 |
| Text | 显示的文本。在你想要用作项目加速键（如果有）的字符之前放置一个安培符号 `&`。例如，如果你将项目设置为 `&Open`，则该项目在菜单中显示为 `Open`，用户可以在菜单打开时按 `Alt+O` 激活它。 |

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_114_0.png)

图 5-4

### 必要的省略号

> 根据惯例，如果菜单项打开了对话框或需要用户进行其他输入后才能继续，其文本应该以省略号 `...` 结尾。如果菜单项立即启动操作，则不应包含省略号。

例如，`Open...` 菜单会显示文件打开对话框，因此它的标题以省略号结尾。相比之下，编辑中的 `Copy`（复制）项会立即复制选中的文本，因此不需要省略号。

加速键 `Accelerators` 允许用户使用键盘而不是鼠标导航。当用户按下 `Alt` 键时，菜单项的加速键下方显示下划线。例如，如果文件菜单显示为 `File`，用户可以按 `Alt+F` 打开菜单，然后使用其他加速键选择菜单项。

> 注意：新版本的 Windows 操作系统通常在按下 `Alt` 键之前不会为加速键加下划线。

你应该为程序的大部分甚至几乎所有的菜单、子菜单和菜单项提供加速键。经验用户通常可以使用加速键比使用鼠标更快地导航菜单系统。

> 警告 确保不要给同一个菜单中的两个项目分配相同的加速键字符。例如，在文件菜单中，不要同时拥有 `Save`（保存）和 `Save As`（另存为）菜单项。

快捷键 `Shortcuts` 允许用户立即激活菜单项。例如，在许多程序中，`Ctrl+O` 打开文件，`Ctrl+S` 保存当前文件。（你可以意识到 `accelerator`（加速键）和 `Alt` 键都以字母 `a` 开头，从而记住它们之间的区别。）

> 警告 务必确保不要给两个菜单项设置相同的快捷键！

> 提示 使用标准的加速键和快捷键帮助用户快速且准确地学习如何使用你的应用程序。网页 `.microsoft.com/kb/126449` 和 `windows.microsoft.com/en-us/windows/keyboard-shortcuts` 列出了微软使用的一些快捷键。我还没有见过一份好的标准加速键列表，但你可以尝试参考其他常用应用程序（如 `Visual Studio` 和 `Word`）中使用的加速键。

## 处理菜单事件

当用户点击菜单时，该控件会像点击按钮一样抛出 `Click` 事件，你可以以相同的方式处理它。你甚至可以以相同的方式创建默认事件处理器：通过双击控件。

## 创建右键菜单

当你右键点击特定控件时，会出现上下文菜单。在 Windows Forms 应用程序中，使用上下文菜单与使用主菜单一样简单。图 5-5 显示了显示上下文菜单的示例。

从表单上拖入一个 `ContextMenuStrip`。与 `MenuStrip` 一样，`MenuStrip` 会出现在表单下方的组件区 `Component Tray` 中，因此你可以双击工具箱中的 `ContextMenuStrip` 工具，而无需担心它的位置。

与 `MenuStrip` 不同，`MenuStrip` 会出现在表单下方的组件区中，因此你可以双击工具箱中的 `ContextMenuStrip` 工具，而无需担心它的位置。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_116_0.png)

图 5-5

与 `MenuStrip` 不同，`MenuStrip` 会出现在表单下方的组件区中，因此你可以双击工具箱中的 `ContextMenuStrip` 工具，而无需担心它的位置。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_116_1.png)

图 5-6

手势非常强大，但它们也很复杂，因此我不会在这本书中介绍它们。你可以在 `mdn.microsoft.com/en-us/library/ms7523068` 中的“Commanding Overview”文章中了解更多相关信息。

同时，你只需为菜单项创建 `Click` 事件处理程序。

### 尝试一下

在本次尝试中，你将创建一个主菜单和一个右键菜单。主菜单包含一个关闭表单的退出 `Exit` 命令。两个菜单都包含更改表单上 `TextBox` 外观的命令。图 5-8 显示了显示其右键菜单的完成程序。

![](img/73c7d7cb173bc2ebb3d8a9797355a5f3_119_0.png)

图 5-8

## 课程要求

在本节中，你将：

- 创建如图5-8所示的所示。

- 创建以下主菜单结构（注意加速键和快捷键）：

文件

退出

格式

颜色

红色 `Ctrl+R`

绿色 `Ctrl+G`

蓝色 `Ctrl+B`

背景颜色

粉色

浅绿色

浅蓝色

| 小号 | `Ctrl+S` |

| 普通 | `Ctrl+N` |

| 大 | `Ctrl+L` |

- 为主菜单项添加后台代码。

- 使右键菜单复制主菜单的“格式”子菜单。

- 将右键菜单绑定到与主菜单相同的事件处理程序上。

- 将右键菜单绑定到 `TextBox`。

> 注意：你可以从 `www.wrox.com/csharp24hourtrainer2e` 网站下载本节课程的代码和资源。

## 提示

- 退出菜单项可以通过调用 `this.Close()` 来关闭程序。

- 创建字体并不是易事（我还没有介绍这一部分）。更简单的方法是在表单上的控件中保留字体样本，然后将 `TextBox` 的 `Font` 属性设置为该控件的 `Font` 属性。还有什么地方比主菜单项更适合存储字体呢？

## 步骤详解

- 创建如图5-8所示的表单。

1. 通过双击工具箱中的 `MenuStrip` 创建主菜单。

2. 在表单上添加一个 `TextBox`。在其 `Text` 属性中输入一些文本，并设置其属性：`Name = contentsTextBox`，`MultiLine = True`，`Dock = Fill`，`ScrollBars = Both`。

3. 通过双击工具箱中的 `ContextMenu` 工具创建右键菜单。

创建主菜单结构。

1. 选择 `MenuStrip`。点击“在此处输入”框并输入 `E&File`。

2. 在 `File` 菜单下方的“在此处输入”框中输入 `E&xit`。

> 根据惯例，退出命令使用 `X` 作为其加速键。它从没有快捷键，因为在对着键盘撞头时（或者手指按错、键盘被飞过的网球撞到，或者你的猫走过键盘）很容易意外关闭程序。

3. 再次点击 `File` 项。在右侧的“在此处输入”框中输入 `F&format`。（你不能使用 `F` 作为此菜单的加速键，因为它已经被 `File` 项使用。）

4. 使用 `Format` 菜单下方的“在此处输入”框创建格式菜单项和子菜单。

5. 使用属性窗口将 `Font` 菜单中 `Small`、`Normal` 和 `Large` 项的字体大小设置为 6、9 和 20。

6. 给 `Color` 和 `Font` 子菜单项赋予适当快捷键。

7. 给执行操作的菜单项赋予适当名称。例如，将 `Font` 菜单的 `Small` 命名为 `formatSmallMenuItem`。

为主菜单项添加后台代码。

1. 双击 `Exit` 项并在代码中输入**粗体行**，使事件处理程序看起来如下：

```java
private void fileExitMenuItem_Click(object sender, EventArgs e)
{
    this.Close();
}
```

关键字 `this` 意味着“当前执行此代码的对象”，在例例中意味着当前表单，因此此行代码告诉当前表单关闭自己。

2. 双击 `Color Red` 项并在以下代码中输入**粗体行**，使事件处理程序看起来如下：

```java
private void formatColorRedMenuItem_Click(object sender, EventArgs e)
{
    contentsTextBox.ForeColor = Color.Red;
}
```

3. 对 `Green` 和 `Blue` 菜单项重复步骤 2。

4. 对 `Format Background` 菜单项重复步骤 2。

5. 双击 `Format Small` 项并在以下代码中输入**粗体行**，使事件处理程序看起来如下：
